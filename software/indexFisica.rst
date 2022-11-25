Cluster Físcia teorica 
#################

**Python**
*********

`Python <https://www.python.org/about/>` es un lenguaje de programación de alto nivel comunmente usado por su sintaxis facil de entender y la gran cantidad de modulos disponibles (como por ejemplo NumPy o TensorFlow)

Para usar Python en el cluster, lo más aconsejable es crear un entorno virtual usando `Anaconda <https://www.anaconda.com//>`, de esta manera el usuarario tendrá control sobre la versión de Python y podrá instalar las librerías que necesite. 

Uso de Conda
================================

Para crear un entorno virtual de Python primero debemos cargar el módulo Anaconda y luego creamos el entorno virtual, para ello ejecutamos la siguiente siguiente serie de comandos (para usar python 2 cargue Anaconda2 y para usar python 3 cargue Anaconda3)::
 
 [dgarzona@hercules8 ~]$ module avai
 [dgarzona@hercules8 ~]$ module load envs/anaconda3
 (base) [dgarzona@hercules8 ~]$ conda create --name my-env python=3.10
 (base) [dgarzona@hercules8 ~]$ conda activate my-env
 (my-env) [dgarzona@hercules8 ~]$ 

Una vez activado el entorno virtual, puede instalar modulos de usando el comando pip:: 

 (my-env) [dgarzona@hercules7 ~]$ pip install numpy
 (my-env) [dgarzona@hercules7 ~]$ pip install pandas

Cuando ya instale todos los modulos que necesite usted puede ejecutar Scripts de Python de dos maneras::

1. En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas. 
2. Mediante el envío de scripts donde se agenda su trabajo para ser ejecutado; normalmente son trabajos que reservan y usan los recursos entre 8 horas hasta 15 días o lo asignado al proyecto del usuario.

Ejecutar Python en una sesion Interactiva vía SRUN
================================

Este procedimiento no requiere de agendamiento para reservar los recursos con los que ejecutará los procesos;  Siempre y cuando esten disponibles y su programa no requiera mas de tres(3) horas reloj pared -- `wall-clock <https://en.wikipedia.org/wiki/Elapsed_real_time#:~:text=Elapsed%20real%20time%2C%20real%20time,at%20which%20the%20task%20started.>`_  -- de procesamiento; se ejecutará inmediatamente.

Luego de conectarse con una sesion ssh en el nodo de logueo del cluster biocomputo o usando el nodo de logueo de la Federación de clusters, debe solicitar los recursos en una sesion interactiva usando el commando SRUN.::

Para ello debe ejecutar el siguiente comando:

 [dgarzona@hercules6]$ srun -p cpu.HigMem.q* --pty /bin/bash -i
 [dgarzona@hercules6]$ module avai
 [dgarzona@hercules6]$ module load envs/anaconda3
 (base) [dgarzona@hercules8 ~]$ conda activate my-env
 (my-env) [dgarzona@hercules8 ~]$ cd "ruta de la carpeta con el script"
 (my-env) [dgarzona@hercules8 ~]$ python3 example.py

Ejecutar Python solicitando los recursos y agendando la ejecucion via scripts
=============================================

Crear un script para correr Python
----------------------------------------
Para enviar su trabajo puede hacer un script de shell con algunas directivas que especifican la cantidad de CPU, memoria, tiempo a usar, número de nodos, etc., que el sistema interpretará al enviarlo con el comando *sbatch*.::

Para ejecutar Python el script *run_python.sh* podría contener::

 #!/bin/bash -l
 #SBATCH --job-name=anvio      #Nombre del Trabajo
 #SBATCH -n 1  #solicita reservar  4 Core de CPU  
 #SBATCH -N 1  #solicita asignar un(1) nodo de computo donde esten disponibles 4 cores(linea anterior).
 #SBATCH -w hercules2 #El nodo que reserva para realizar su trabajo
 #SBATCH -t 0-00:60    #Su trabajo se ejecutara por 60 minutos, luego se eliminara; aun si no se completa.
 #SBATCH -p cpu.normal.q     #Esta linea indica la particion de la cual se seleccionara los nodos requeridos.
 #SBATCH --mem-per-cpu=4000    #Usted reservara 4G de memoria RAM por Tarea o Core de CPU.
 #SBATCH -o python_%j.out      #La salida de su trabajo sera redireccionada al archivo output_*JOBID*.txt
 #SBATCH -e python_%j.err       #La salida de errores de su trabajo sera redireccionada al archivo  error_JOBID.txt
 module load envs/anaconda3
 conda activate my-env
 python3 example.py

Después puede agendar su ejecución con::

 sbatch -M biocomputo run_python.sh
