Cluster Físcia teorica 
#################

**Python**
*********

`Python <https://www.python.org/about/>` es un lenguaje de programación de alto nivel comunmente usado por su sintaxis facil de entender y la gran cantidad de modulos disponibles (como por ejemplo NumPy o TensorFlow)

Para usar Python en el cluster, lo más aconsejable es crear un entorno virtual usando `Anaconda <https://www.anaconda.com//>`, de esta manera el ususrario tendra control sobre la versión de python y podrá instalar las librerías que necesite. 

Uso de Conda
================================

Para crear un entorno virtual de Python primero debemos cargar el modulo de Anaconda y luego creamos el entorno virtual, para ello ejecutamos la siguiente siguiente serie de comandos (para usar python 2 cargue Anaconda2 y para usar python 3 cargue Anaconda3): 
 [dgarzona@hercules8 ~]$ module avai
 [dgarzona@hercules8 ~]$ module load envs/anaconda3
 (base) [dgarzona@hercules8 ~]$ conda create --name my-env python=3.10
 (base) [dgarzona@hercules8 ~]$ conda activate my-env
 (my-env) [dgarzona@hercules8 ~]$ 

Una vez activado el entorno virtual, puede instalar modulos de usando el comando pip: 
 (my-env) [dgarzona@hercules7 ~]$ pip install numpy
 (my-env) [dgarzona@hercules7 ~]$ pip install pandas

Cuando ya instale todos los modulos que necesite usted puede ejecutar Scripts de Python de dos maneras:

1. En una sesion iteractiva donde los resultados se esperan en tiempos no mayores a tres(3) horas. 
2. Mediante el envío de scripts donde se agenda su trabajo para ser ejecutado; normalmente son trabajos que reservan y usan los recursos entre 8 horas hasta 15 días o lo asignado al proyecto del usuario.



 

