

**Cluster Biologia Computacional**
***********************************

Anvio7.1
====
`ANVIO <https://anvio.org/>`_  es una plataforma de software que usa estrategias computacionales extendidas a la microbiología junto a datos obtenidos de areas como la genómica, metagenómica, metatranscriptómica, pangenómica, metapangenómica, filogenómica y la genética de poblaciones microbianas en una manera integrada y fácil de usar a través de capacidades de visualización interactiva.

.. note:: El container con ANVIO7.1 esta en: **/localapps/anvio_7.1_main_0522.sif** .

Usted puede ejecutar anvio_7.1  en la Federacion de cluster  de dos maneras:

1.  En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas y, 
2. mediante el envio de scripts donde se agenda su trabajo para ser  ejecutado; normalmente son trabajos que reservan y usan los recursos entre 8 horas hasta 15 dias o lo asignado al  proyecto del usuario.
  
Ejecutar ANVIO en una sesion Interactiva via SRUN
================================
Este procedimiento no requiere de agendamiento para reservar los recursos con los que ejecutara los procesos;  Siempre y cuando esten disponibles y su programa no requiera mas de tres(3) horas reloj pared -- `wall-clock <https://en.wikipedia.org/wiki/Elapsed_real_time#:~:text=Elapsed%20real%20time%2C%20real%20time,at%20which%20the%20task%20started.>`_  -- de procesamiento; se ejecutara inmediatamente.

Luego de conectarse con una sesion ssh en el nodo de logeo del cluster biocomputo o usando el nodo de logeo de la Federacion de clusters, debe solicitar los recursos en una sesion interactiva usando el commando SRUN.

**Si inicia sesion desde el nodo de la federacion** debe adicionar el parametro -M *NombreCluster*, tambien deberia adicionar el parametro que indica el grupo de nodos --o particion-- a los que va acceder con -p *NombreParticion*.  En el ejemplo que sigue se reserva todos los recursos de un(1) nodo del grupo o particion "cpu.normal.q",  en el cluster "biocomputo" asi::

 *srun -M biocomputo -p cpu.normal.q --pty /bin/bash -i*
 
Si usted se **accedio a un cluster asociado **,  los recursos se reservan en el cluster al que pertenece el nodo donde ingresa:: 
 
 srun -p cpu.normal.q --pty /bin/bash -i
 
Para usar el software ANVIO7.1 desde el container, debera informar a  singularity los directorios a los que  requiere tener acceso; la variable *SINGULARITY_BINDPATH*  almacena estas rutas(path). 

Si usa bash puede hacerlo asi::

  export  SINGULARITY_BINDPATH="/scratchsan/acaroq/divanegasa"

Luego ejecute *singularity* para iniciar una *shell* en el software del container::

   *singularity shell /localapps/anvio_7.1_main_0522.sif*
   
El cambio en el prompt  a "Singularity>" indica que  ingreso al container
   
Tutorial con Anvio7.1 en el Cluster biocomputo
-----------------------------------------

El tutorial sigue lo propuesto por  ANVIO  en:
 *https://merenlab.org/tutorials/read-recruitment/*

Los datos usado son obtenidos de simulaciones e incluyen una secuencia Referencia y lecturas cortas que, es lo habitual en este tipo de analisis.

El objetivo principal del análisis  es identificar  y clasificar las secuencias presentes en las lecturas cortas  de una muestra de la que se tiene  una secuencia referencia. 

El conjunto de secuencias referencia son un FASTA, pueden representar uno o más segmentos contiguos de ADN (contigs) que, podrian pertenecer a uno o varios genomas y abarcan genes, genomas ensamblados en metagenomas parciales o completos, genomas amplificados individualmente, genomas aislados, genomas virales o plásmidos: Una secuencia  más larga que las lecturas cortas a usar sirve como referencia.

El conjunto de lecturas cortas pudo haberse originado en la secuenciación de un solo genoma, un metagenoma completo o incluso amplicones generados con sus primers; no es necesario que sean lecturas cortas, se pueden incluir lecturas largas con sus secuencias de referencia.

Hay mucha libertad para definir el contexto de su secuencia de referencia y lecturas cortas según la pregunta que desea responder. Pero  cuando se contextualiza correctamente una lectura  puede responder muchas preguntas en microbiología.

A favor de la simplicidad comenzaremos con un ejemplo sencillo: un solo genoma y un conjunto de metagenomas simulados, ya que el propósito del tutorial es ofrecer una vision práctica para identificar las lecturas, hasta donde  la ciencia lo permite.

Primero vaya al directorio asignado en /scratchsan -no use su $HOME--
descargue alli las lecturas comprimidas, descomprimalas.  Ingrese al directorio donde expandio las lecturas: Encontrara el archivo genome.fa que es la secuencia referencia y el directorio metagenomes que incluye varios metagenomas simulados; supondremos son metagenomas intestinales de humanos::
 [divanegasa@perseus ~]$ srun -M biocomputo -p cpu.normal.q -w hercules2 --pty /bin/bash -i
 [divanegasa@hercules2 ~]$ cd /scratchsan/acaroq/divanegasa/
 [divanegasa@hercules2 ~]$ curl -L https://figshare.com/ndownloader/files/31180186 -o metagenomic-read-recruitment-data-pack.tar.gz
 [divanegasa@hercules2 ~]$ tar -zxvf metagenomic-read-recruitment-data-pack.tar.gz
 [divanegasa@hercules2 ~]$ cd metagenomic-read-recruitment-data-pack

 
Preparacion de las lecturas
---------------------------
Para trabajar con las lecturas se requiere ingresar al container y usar el software ANVIO7.1 sobre los datos descargados y expandidos en el anterior procedimiento.  Primero, construiremos una una base de datos con el genoma referencia para sobre ella realizar una anotacion funcional de los genes: identificandolos y usando solo una sola copia del gen al que se adjunta información taxonómica::

 [divanegasa@hercules2 ~]$ export SINGULARITY_BINDPATH="/scratchsan:/scratchsan"
 [divanegasa@hercules2 ~]$ singularity shell /localapps/anvio_7.1_main_0522.sif
  
Se requiere construir una base de datos con el genoma referencia para sobre ella realizar una anotacion funcional de los genes: identificandolos y usando solo una sola copia del gen al que se adjunta información taxonómica::

 Singularity> cd /scratchsan/acaroq/divanegasa/
 Singularity> cd metagenomic-read-recruitment-data-pack
 Singularity> anvi-gen-contigs-database -f genome.fa -o genome.db
 Singularity> anvi-run-ncbi-cogs -c genome.db --num-threads 4
 Singularity> anvi-run-hmms -c genome.db
 Singularity> anvi-run-scg-taxonomy -c genome.db --num-threads 4
 
Una segunda base de datos con el genoma referencia sera contruida con bowtie2 para realizar el mapeo de las lecturas y obtener los alineamientos en un archivo SAM. luego ahorrar espacio transformandolo a BAM indexado y ordenado en donde los alineamientos sran perfilados y visualizados con ANVIO


 Singularity> bowtie2-build genome.fa genome
 Singularity> bowtie2 -x genome -1 metagenomes/magdalena-R1.fastq -2 metagenomes/magdalena-R2.fastq -S magdalena.sam
 Singularity> samtools view -F 4 -bS magdalena.sam -o magdalena-RAW.bam
 Singularity> samtools sort magdalena-RAW.bam -o magdalena.bam
 Singularity> samtools index magdalena.bam
 Singularity> anvi-profile -i magdalena.bam -c genome.db -o magdalena-profile --cluster

Los resultados los puede visualizar en un navegador con la URL  http://0.0.0.0:8080 del nodo donde realiza los calculos.

Ejecutar ANVIO7.1 solicitando los recursos y agendando la ejecucion via scripts
=============================================
En la federacion de Cluster del CECC los recursos son aportados por los cluster asociados y se comparten  entre los usuarios,  para garantizar un uso justo, todos deben realizar el envio de trabajos a través del sistema por lotes que ejecutará las aplicaciones en los recursos disponibles.

Crear un script para correr ANVIO7.1
----------------------------------------
Para enviar su trabajo puede hacer un script de shell con algunas directivas que especifican la cantidad de CPU, memoria, tiempo a usar, numero de modos, etc., que el sistema interpretará al enviarlo con el comando sbatch.

Para ejecutar gaussian el script *run_anvio.sh*  podria contener::
  
 #!/bin/bash -l
 #SBATCH --job-name=anvio      #Nombre del Trabajo
 #SBATCH -n 4  #solicita reservar  4 Core de CPU  
 #SBATCH -N 1  #solicita asignar un(1) nodo de computo donde esten disponibles 4 cores(linea anterior).
 #SBATCH -w hercules2 #El nodo que reserva para realizar su trabajo
 #SBATCH -t 0-00:60    #Su trabajo se ejecutara por 60 minutos, luego se eliminara; aun si no se completa.
 #SBATCH -p cpu.normal.q     #Esta linea indica la particion de la cual se seleccionara los nodos requeridos.
 #SBATCH --mem-per-cpu=4000    #Usted reservara 4G de memoria RAM por Tarea o Core de CPU.
 #SBATCH -o anvio_%j.out      #La salida de su trabajo sera redireccionada al archivo output_*JOBID*.txt
 #SBATCH -e anvio_%j.err       #La salida de errores de su trabajo sera redireccionada al archivo  error_JOBID.txt
 #SBATCH --mail-type=BEGIN,END #Se enviara un e-mail cuando Inicie y finalice su trabajo.
 #SBATCH --mail-user=test@unal.edu.co  #El correo donde se enviaran notificaciones cuando inicie y finalice el trabajo.

       unset SINGULARITY_BINDPATH  #remuevo atributos y valores de la variable *SINGULARITY_BINDPATH*
       export SINGULARITY_BINDPATH="/scratchsan:/scratchsan"  #Permite acceso al directorio /scratchsan vinculandolo al directorio /scratchsan  dent$
       singularity exec  /localapps/anvio_7.1_main_0522.sif /bin/sh script.sh  #Desde el container, ejecuto el contenido del  script script.sh
   
   
El contenido de script.sh puede incluir la mayoria de las lineas ejecutadas de modo iteractivo::
 #!/bin/bash
        cd /scratchsan/acaroq/divanegasa/
        cd metagenomic-read-recruitment-data-pack
          anvi-gen-contigs-database -f genome.fa -o genome.db
          anvi-run-ncbi-cogs -c genome.db --num-threads 4
          anvi-run-hmms -c genome.db
          anvi-run-scg-taxonomy -c genome.db --num-threads 4
             bowtie2-build genome.fa genome
             bowtie2 -x genome -1 metagenomes/magdalena-R1.fastq -2 metagenomes/magdalena-R2.fastq -S magdalena.sam
             samtools view -F 4 -bS magdalena.sam -o magdalena-RAW.bam
             samtools sort magdalena-RAW.bam -o magdalena.bam
             samtools index magdalena.bam
             anvi-profile -i magdalena.bam -c genome.db -o magdalena-profile --cluster


Después puede agendar su ejecucion  con::
	sbatch -M biocomputo run_anvio.sh

Los resultados los puede visualizar en un navegador con la URL  http://0.0.0.0:8080 del nodo donde realiza los calculos.




