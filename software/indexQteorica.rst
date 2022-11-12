.. _Softwareqteorica:

Cluster Quimica Teorica
#################
**gaussian**
*********
`gaussian 16 <https://gaussian.com/g16main/>`_ es un conjunto de herramientas de software para el modelamiento de estructuras electronicas en sistemas moleculares. 

.. note:: El container con gaussian16 esta en: **/localapps/centos7.gaussian16.sif** .

Usted puede correr gaussian16  en la Federacion de cluster  de dos maneras:

1.  En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas y, 
2. mediante el envio de scripts donde se agenda su trabajo para ser  ejecutado; normalmente son trabajos que reservan y usan los recursos entre 8 horas hasta 15 dias o lo asignado al  proyecto del usuario.
  
Ejecutar gaussian16 en una sesion Interactiva via SRUN
================================
Este procedimiento no requiere de agendamiento para reservar los recursos con los que ejecutara los procesos;  Siempre y cuando esten disponibles y su programa no requiera mas de tres(3) horas reloj pared -- `wall-clock <https://en.wikipedia.org/wiki/Elapsed_real_time#:~:text=Elapsed%20real%20time%2C%20real%20time,at%20which%20the%20task%20started.>`_  -- de procesamiento; se ejecutara inmediatamente.

Luego de conectarse en una sesion --shell-- en el nodo de logeo del cluster qteorica o usando el nodo de logeo de la Federacion de clusters, debe solicitar los recursos en una sesion interactiva usando el commando SRUN.

**Si inicia sesion desde el nodo de la federacion** debe adicionar el parametro -M *NombreCluster*, tambien deberia adicionar el parametro que indica el grupo de nodos --o particion-- a los que va acceder con -p *NombreParticion*.  en el ejemplo que sigue se reserva todo los recursos de un(1) nodo del cluster "irlande":

.. sidebar:: SRUN 
    srun envia un trabajo y lo ejecuta en tiempo real
   
    Para ejecutar una trabajo con srun en un cluster especifico, debe adicionar el parametro
     *-M NombreCluster*
 
**srun -M irlande -p cpu.HigMem.q --pty /bin/bash -i**
 
Si usted se **logeo en  un cluster asociado**  por omision los recursos se reservan en el cluster al que pertenece el nodo donde se logea. 
 
**srun -p debug --pty /bin/bash -i**
    
Una vez inicie una sesion interactiva(-i) puede ejecutar el container 
 

 **Correr el container con gaussian16 una sesion Interactiva usando srun**
 ******************************************************************************

Para usar el software gaussian16 desde el container, debera informar a  singularity los directorios a los que  requiere tener acceso; la variable *SINGULARITY_BINDPATH*  almacena estas rutas(path).  Adicionalmente debe dar un valor a la variable GAUSS_SCRDIR que indica el directorio donde se almacenaran los archivos temporales.

Si usa bash puede hacerlo asi::

  export  SINGULARITY_BINDPATH="/home/qteorica:/home/qteorica"
  export GAUSS_SCRDIR="/home/qteorica/scratchsan"

En *sh puede hacerlo asi::

  setenv SINGULARITY_BINDPATH /home/qteorica:/home/qteorica
  setenv GAUSS_SCRDIR /home/qteorica/scratchsan

Luego ejecute *singularity* para usar una sesion *shell* y el software del container::

   singularity shell /localapps/centos7.gaussian16.sif
   
   El cambio en el prompt le indica que  ingreso alcontainer
   "Singularity>"
 
Una vez en el container, puede correr gaussian16.  p. ejem::
    *g16* < test0001.com >test0001.com.out

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
