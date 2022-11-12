.. _Software:
********
Software
********
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


Cluster Quimica Teorica
#################
**gaussian**
*********
`gaussian 16 <https://gaussian.com/g16main/>`_ es un conjunto de herramientas de software para el modelamiento de estructuras electronicas en sistemas moleculares. 

.. note:: El container con gaussian16 esta en: **/localapps/centos7.gaussian16.sif** .

Usted puede correr gaussian16  en la Federacion de cluster  de dos maneras:

1.  En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas y, 
2. mediante el envio de scripts donde se agenda su trabajo para ser  ejecutado; normalmente son trabajos que reservan y usan los recursos entre 8 horas hasta 15 dias o lo asignado al  proyecto del usuario.
  
 **Ejecutar gaussian16 en una sesion Interactiva via SRUN**
Este procedimiento no requiere de agendamiento para reservar los recursos con los que ejecutara los procesos;  Siempre y cuando esten disponibles y su programa no requiera mas de tres(3) horas reloj pared -- `wall-clock <https://en.wikipedia.org/wiki/Elapsed_real_time#:~:text=Elapsed%20real%20time%2C%20real%20time,at%20which%20the%20task%20started.>`_  -- de procesamiento; se ejecutara inmediatamente.

Luego de conectarse en una sesion --shell-- en el nodo de logeo del cluster qteorica o usando el nodo de logeo de la Federacion de clusters, debe solicitar los recursos en una sesion interactiva usando el commando SRUN.

Si inicia desde el nodo de la federacion debe adicionar el parametro -M NombreCluster, tambien deberia adicionar el parametro que indica el grupo de nodos --o particion-- a los que va acceder con -p NombreParticion.  en el ejemplo que sigue se reserva todo los recursos de un(1) nodo:

.. sidebar:: SRUN 
    :subtitle: srun envia un trabajo y lo ejecuta en tiempo real
   
    Para enviar un trabajo a procesar en un nodo disponible en un cluster de  la Federacion debe adicionar el parametro **-M Nombre_Cluster**
    **srun -M qteorica -p debug --pty /bin/bash -i**
 
Si usted se logeo al nodo control del cluster qteorica no requiere indicar en que cluster desea reservar recursos, por omision los recursos se reservan en el cluster al que pertenece el nodo donde se logea. En el ejemplo se reserva todo los recursos de un nodo en el cluster al que pertenece el mismo nodo.
 
srun -p debug --pty /bin/bash -i
    
Una vez inicie una sesion interactiva(-i) puede ejecutar el container 
 

 **Correr el container con gaussian16 en l+------------------a sesion Interactiva con menos de 3 horas de reloj de pared(wallclock)**

Para ejecutar el container con gaussian16 se usa el software singularity.
Usted debe primero informar a  singularity los directorios a los que requiere tener acceso desde ele container usando la variable *SINGULARITY_BINDPATH*.  Usted no requiere pasar un valor a esta variable si solo va usar su directorio de trabajo o *$HOME*.  Adicionalmente Tambien debe dar un valor a la variable GAUSS_SCRDIR que asigna el directorio donde se almacenaran los archivos de procesos intermedios(scratch),  

P. eje., 
El usuario tiene su $HOME en  /home/qteorica/
El archivo de entrada al programa se llama "test0001.com" y esta en la ruta /home/qteorica/Basic_scripts_SLURM
El directorio  "GAUSS_SCRDIR" a usar tien la ruta(path) /home/qteorica/scratchsan

Debido a que en este ejemplo Todo lo trabajo en el $HOME del usuario, no requiero pasar un valor a *SINGULARITY_BINDPATH*, o No tiene efecto en el proceso  si le asigno el valor de mi $HOME:
 export  SINGULARITY_BINDPATH="/home/qteorica:/home/qteorica"
En este ejemplo mi  "GAUSS_SCRDIR" es la ruta /home/qteorica/scratchsan
export GAUSS_SCRDIR="/home/qteorica/scratchsan"

Luego inicio una sesion shell en el container de gaussian

singularity shell /localapps/centos7.gaussian16.sif
Usted vera el cambio en el prompt cuando ha ingresado al container
Singularity>
