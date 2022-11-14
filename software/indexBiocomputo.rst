
.. _indexBiocomputo

Cluster Biologia Computacional
#################
**orthofinder**
*********
`Orthofinder <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1832-y>`_ es un software para inferencia filogenetica de ortologos, arboles de genes y especies  con unico nodo( rooted), eventos de duplicacion de genes y estadistica de genomica comparativa.

En el cluster de Biologia Computacional el software Orthofinder  y sus dependencias necesarias se encuentran almacenados en una entidad llamada container (que incluye un sistema operativo minimo).  Esta pieza unica o imagen(un archivo) se encuentra "lista para correr", es portable y se puede compartir a tiempo que los resultados son reproducibles.

Usted puede correr Ortofinder en el cluster de Biologia Computacional de por lo menos dos maneras:

1.  En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas y 
2. mediante scripts donde usted envia un trabajo que en entra a ser agendado y luego ejecutado; puede tomar mas de una(1) semana.
  
 **Correr Orthofinder en una sesion Interactiva via SRUN**
Este procedimiento no requiere de un agendamiento para ejecutar sus procesos y disponer de los recursos(procesador, Memoria Ram, Discos de almacenamiento):  Siempre y cuando se encuentren disponibles y su programa no requiera mas de tres(3) horas de procesamiento.

 Primero, usted debe conectarse y abrir una sesion shell en el nodo "hercules1" del laboratorio de Biologia computacional.
 
 Luego debe iniciar una sesion interactiva con uno de los nodos de procesamiento del cluster  con el commando SRUN asi:
 
 .. image:: /images/srun_orthocluster.png
    :width: 680px
    :align: left
    :height: 100px
    :alt: runOrthocluster
    
Una vez se inicie una sesion interactiva con un nodo del cluster, usted puede ejecutar el container orthofinder, ubicado en:
       ``/localapps/orthofinder_2.5.4.sif``

 **Correr el container Orthofinder en la sesion Interactiva**

Para ejecutar el container orthofinder_2.5.4 se usa el software singularity.
Usted debe primero comunicar a  singularity los directorios en los que trabajara usando la variable *SINGULARITY_BINDPATH* 

Por omision usted no requiere dar ningun valor a esta variable si solo va usar su directorio de trabajo o *$HOME*.

Si, por ejemplo desea trabajar en un directorio /scratchsan debe incluirlo en la variable *SINGULARITY_BINDPATH* asi:

 .. image:: /images/run_singularity_orthocluster.png
    :width: 680px
    :align: left
    :height: 100px
    :alt: runOrthocluster
 
 Luego ejecute singularity para  acceder a la shell del container.
 
  .. image:: /images/run_singularity_orthocluster_shell.png
    :width: 680px
    :align: left
    :height: 100px
    :alt: runOrthocluster
    
Ejemplo 1:  Del tutorial en (https://davidemms.github.io/orthofinder_tutorials/running-an-example-orthofinder-analysis.html) 
 
 a.  Descargar los proteomas para el conjunto de especies raton, humano, rana, zebrafish, puffer Japones (Takifugu rubripes) and Mosca de la fruta (Drosophila melanogaster).
 
 Creamos la carperta Proteomas por. eje en /scrtchsan/eparra/
 vaya a https://www.ensembl.org/, como el primer sitio para buscar proteomas.
 Orthofinder requiere como entrada seciencias de aminoacidos para todas las proteinas codificadas desde genes en las especies de interes. Las secuencias dben estar en archivos separados con la extension .fa, .faa, .fasta .fas o .pep
 Los archivos que se requieren de descarga en la carpeta creada asi
 
 Humano, archivo fasta de proteinas
  http://ftp.ensembl.org/pub/release-107/fasta/homo_sapiens/pep/Homo_sapiens.GRCh38.pep.all.fa.gz 
 
 Raton, Archivo fasta de proteinas
 
http://ftp.ensembl.org/pub/release-107/fasta/mus_musculus/pep/Mus_musculus.GRCm39.pep.all.fa.gz

Zebrafish, Archivo fasta de Proteina
http://ftp.ensembl.org/pub/release-107/fasta/danio_rerio/pep/Danio_rerio.GRCz11.pep.all.fa.gz

Tropical clawed frog
http://ftp.ensembl.org/pub/release-107/fasta/xenopus_tropicalis/pep/Xenopus_tropicalis.UCB_Xtro_10.0.pep.all.fa.gz

Takifugu rubripes>
http://ftp.ensembl.org/pub/release-107/fasta/takifugu_rubripes/pep/Takifugu_rubripes.fTakRub1.2.pep.all.fa.gz

Drosophila melanogaster
http://ftp.ensembl.org/pub/release-107/fasta/drosophila_melanogaster/pep/Drosophila_melanogaster.BDGP6.32.pep.all.fa.gz

Descomprimo los archivos.

las fasta descargados pueden contener muchos transcritos por gen, correr onrtofinder sobre todos los archivos podria tomar mucho tiempo, ortofinder provee un script que filtra unicamente los trasncritos mas largos por gen y sobre ellos se correra orthofinder

for f in *.fa; do python /opt/OrthoFinder/tools/primary_transcript.py $f; done 

Como los nombres archivos son usados para referirse a alas especies,  es mas facil hacer referencia a anombres cortos.

**ANVIO 7.1**
*********
`ANVIO <https://anvio.org/>`_  es una plataforma de software que usa estrategias computacionales extendidas a la microbiología junto a datos obtenidos de areas como la genómica, metagenómica, metatranscriptómica, pangenómica, metapangenómica, filogenómica y la genética de poblaciones microbianas en una manera integrada y fácil de usar a través de capacidades de visualización interactiva.

.. note:: El container con ANVIO7.1 esta en: **/localapps/anvio_7.1_main_0522.sif** .

Usted puede ejecutar anvio_7.1  en la Federacion de cluster  de dos maneras:

1.  En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas y, 
2. mediante el envio de scripts donde se agenda su trabajo para ser  ejecutado; normalmente son trabajos que reservan y usan los recursos entre 8 horas hasta 15 dias o lo asignado al  proyecto del usuario.
  
Ejecutar ANVIO en una sesion Interactiva via SRUN
================================
Este procedimiento no requiere de agendamiento para reservar los recursos con los que ejecutara los procesos;  Siempre y cuando esten disponibles y su programa no requiera mas de tres(3) horas reloj pared -- `wall-clock <https://en.wikipedia.org/wiki/Elapsed_real_time#:~:text=Elapsed%20real%20time%2C%20real%20time,at%20which%20the%20task%20started.>`_  -- de procesamiento; se ejecutara inmediatamente.

Luego de conectarse con una sesion grafica en el nodo de logeo del cluster biocomputo o usando el nodo de logeo de la Federacion de clusters, debe solicitar los recursos en una sesion interactiva usando el commando SRUN.

**Si inicia sesion desde el nodo de la federacion** debe adicionar el parametro -M *NombreCluster*, tambien deberia adicionar el parametro que indica el grupo de nodos --o particion-- a los que va acceder con -p *NombreParticion*.  En el ejemplo que sigue se reserva todos los recursos de un(1) nodo del grupo o particion "cpu.normal.q",  en el cluster "biocomputo" 

.. sidebar:: SRUN 
    srun envia un trabajo y lo ejecuta en tiempo real
   
    Para ejecutar una trabajo con srun en un cluster especifico, debe adicionar el parametro
     *-M NombreCluster*
 
**srun -M biocomputo -p cpu.normal.q --pty /bin/bash -i**
 
Si usted se **logeo en  un cluster asociado**  por omision los recursos se reservan en el cluster al que pertenece el nodo donde se logea. 
 
**srun -p cpu.normal.q --pty /bin/bash -i**
    
Una vez inicie una sesion interactiva(-i) grafica puede ejecutar el container 
 

 **Correr el container con ANVIO7.1 en una sesion Interactiva usando srun**
 ******************************************************************************

Para usar el software ANVIO7.1 desde el container, debera informar a  singularity los directorios a los que  requiere tener acceso; la variable *SINGULARITY_BINDPATH*  almacena estas rutas(path). 

Si usa bash puede hacerlo asi::

  export  SINGULARITY_BINDPATH="/home/qteorica:/home/qteorica"
  export GAUSS_SCRDIR="/home/qteorica/scratchsan"

En *sh puede hacerlo asi::

  setenv SINGULARITY_BINDPATH /home/qteorica:/home/qteorica
  setenv GAUSS_SCRDIR /home/qteorica/scratchsan

Luego ejecute *singularity* para iniciar una sesion *shell* en el software del container::

   *singularity shell /localapps/anvio_7.1_main_0522.sif*
   
   El cambio en el prompt  indica que  ingreso al container
   "Singularity>"
 
Una vez en el container, puede correr anvio_7.1

Ejecutar Tutorial con Anvio7.1 en el Cluster biocomputo
-----------------------------------------

En este tutorial se seguida lo propuesto por la documentacion ANVIO  en *https://merenlab.org/tutorials/read-recruitment/*, 

Ejemplo para Incluir en ANVIO  los datos presentes en las lecturas.

El proposito es:
1. Incluir  los datos de lecturas  en  formatos FASTA, FASTQ, SAM y BAM. 
2. Aprenda los pasos básicos del incluir lecturascon Bowtie2 y samtools,
3.  Aprender a perfilar los resultados identificados en la lectura usando anvi'o,
4.  Familiarizarse con los pasos posteriores del análisis de lecturas usadas.

Los datos usado son simulaciones, que incluyen una secuencia Referencia y otras lecturas cortas que es lo habitual par este tipo de analisis.

El objetivo principal de este análisis  es identificar  y clasificar las secuencias presentes en las lecturas cortas  de una muestra de la que se tiene  una secuencia referencia. 

El conjunto de secuencias referenciaestan en un archivo FASTA, pueden ser uno o más segmentos contiguos de ADN (contigs) que, pueden pertenecer a uno o varios genomas que pueden abarcar genes, genomas ensamblados en metagenomas parciales o completos, genomas amplificados individualmente, genomas aislados, genomas virales o plásmidos: Cualquier secuencia que sea más larga que las lecturas cortas usadas aqui puede servir como referencia.

El conjunto de lecturas cortas usado aqui también prodria haberse originado en la secuenciación de un solo genoma, un metagenoma completo o incluso amplicones generados con sus primers. Tampoco es necesarios que sean lecturas cortas, se puede incluir lecturas largas con sus secuencias de referencia.

Esencialmente, tiene mucha libertad para definir su contexto de secuencia de referencia y lecturas cortas según la pregunta que desea responder. Pero  cuando se usa correctamente una lectura contextualizandola puede responder muchas preguntas en microbiología.

A favor de la simplicidad comenzaremos con un ejemplo sencillo: un solo genoma y un conjunto de metagenomas simulados, ya que el propósito de este tutorial es ofrecerle una vision práctica para identificar las lecturas hasta donde  la ciencia lo permite.

Primero vaya al directorio asignado en /scratchsan -no use su $HOME--
descargue alli las lecturas comprimidas, descomprimalas.  Ingrese al directorio donde expandio las lecturas: Encontrara el archivo genome.fa que es la secuencia referencia y el directorio metagenomes que incluye varios metagenomas simulados; supondremos son metagenomas intestinales de humanos.

.. image:: /images/anvio1.png
    :width: 680px
    :align: left
    :height: 100px
    :alt: runOrthocluster

Preparacion
-------------

es necesario hacer una base de datos con el genoma referencia para todos los pasos posteriores con ANVIO, agregamos el parametro --num-threads 8 para agilizar el proceso.

sobre las bases de datos de contigs se una anotacion funcional de los genes: identificandolo y usando solo una sola copia del gen se adjunta información taxonómica.



Ejecutar gaussian16 solicitando los recursos y agendando la ejecucion via scripts
=============================================
En la federacion de Cluster del CECC los recursos son aportados por los cluster asociados y se comparten  entre los usuarios,  para garantizar un uso justo, todos deben realizar el envio de trabajos a través del sistema por lotes que ejecutará las aplicaciones en los recursos disponibles.

Crear un script para correr gaussian16
----------------------------------------
Un script para enviar su trabajo es un script de shell con algunas directivas que especifican la cantidad de CPU, memoria, tiempo a usar, numero de modos, etc., que el sistema interpretará al enviarlo con el comando sbatch.

Para ejecutar gaussian el script *run_gaussian.sh*  podria contener::
  
  #!/bin/bash	#El interprete que su script usa
  #SBATCH --job-name=gauss16	#Nombre del Trabajo
  #SBATCH -n 4	#solicita reservar  4 Core de CPU
  #SBATCH -N 1	#solicita asignar un(1) nodo de computo donde esten disponibles 4 cores(linea anterior).
  #SBATCH -t 0-00:30	#Su trabajo se ejecutara por 30 minutos, luego se eliminara; aun si no se completa.
  #SBATCH -p debug	#Esta linea indica la particion de la cual se seleccionara los nodos requeridos.
  #SBATCH --mem-per-cpu=4000	#Usted reservara 4G de memoria RAM por Tarea o Core de CPU.
  #SBATCH -o output_%j.txt	#La salida de su trabajo sera redireccionada al archivo output_*JOBID*.txt
  #SBATCH -e error_%j.txt 	#La salida de errores de su trabajo sera redireccionada al archivo  error_JOBID.txt
  #SBATCH --mail-type=BEGIN,END	#Se enviara un e-mail cuando Inicie y finalice su trabajo.
  #SBATCH --mail-user=test@unal.edu.co	#El correo donde se enviaran notificaciones cuando inicie y finalice el trabajo.
        
       unset SINGULARITY_BINDPATH  #remuevo atributos y valores de la variable *SINGULARITY_BINDPATH*
       export SINGULARITY_BINDPATH="/homes:/homes"  #Permite acceso al directorio /homes vinculandolo al directorio /homes  dentro del container.
       *singularity exec /localapps/centos7.gaussian16.sif  /bin/sh script.sh* #Desde el container, ejecuto el contenido del  script *script.sh*

El contenido de *script.sh* es::

	#!/bin/bash
   		export GAUSS_SCRDIR="/home/qteorica/scratchsan/"
        		g16 < test0001.com >test0001.com.out

Después puede agendar su ejecucion  con::
	*sbatch -M qteorica run_gaussian.sh*





