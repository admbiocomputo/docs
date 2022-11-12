.. _Softwareqteorica:
********
Software
********
Cluster Quimica Teorica
#################
**gaussian**
*********
`gaussian 16 <https://gaussian.com/g16main/>`_ es un conjunto de herramientas de software para el modelamiento de estructuras electronicas en sistemas moleculares. 

El software se encuentra disponible en:

/localapps/centos7.gaussian16.sif

Usted puede correr gaussian16  en la Federacion de cluster  de dos maneras:

1.  En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas y, 
2. mediante scripts donde usted agenda su trabajo para ser ejecutado; normalmente son trabajos que reservan recursos entre 8 horas hasta 12 dias.
  
 **Ejecutar gaussian16 en una sesion Interactiva via SRUN**
Este procedimiento no requiere de agendamiento para reservar los recursos y ejecutar los procesos;  Siempre y cuando esten disponibles y su programa no requiera mas de tres(3) horas --reloj Pared--de procesamiento se ejecutara inmediatamente.

Primero, usted debe conectarse en una sesion --shell-- en el nodo de control del cluster qteorica o usando el nodo control de la Federacion de clusters.
 
Luego debe solicitar los recursos en una sesion interactiva usando el commando SRUN;  si inicia desde el nodo de la federacion debe adicionar el parametro -M NombreCluster, tambien deberia adicionar el parametro que indica el grupo de nodos --o particion-- a los que va acceder con -p NombrePartion.  en el ejemplo que sigue se reserva todo los recursos de un(1) nodo:
 
 srun -M qteorica -p debug --pty /bin/bash -i
 
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



