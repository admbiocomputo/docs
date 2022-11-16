.. _indexModulos
**Sistema de Modulos**
****************

La mayoria del software no se encuentra en el sistema operativo las rutinas que logran ubicar el software y sus dependencias son gestionadas por los módulos que permiten acceder al software, tener varias versiones de manera concurrente o permitir cambiar entre ellas de modo facil.


Comando `module`
##########

Los modulos  pueden ser llamados por los scripts con los que se envia un trabajo o en una sesion iteractiva.  Existen algunos comando que puede usar en los modulos. 

Para ver los modulos disponible ejecute en una terminal o consola:

```
module avail
```

Esto retornara una lista de los modulos que estan disponible para usar en su sesion; Para cargar el modulo que eligio en su ambiente ejecute::
 module load some_module
 # example: "module load apps/cdhit/4.8.1"


Usando Modulos en un script de trabajo
######################

Los modulos en un script SLURM de trabajo pueden ser llamdos luego de las directivas `#SBATCH` y antes de la linea que lo usara, por ejemplo el siguiente script ejecutara un trabajo cargando python y ejecutando python 3.9::

 #!bin/bash
 #SBATCH --nodes=1
 #SBATCH --time=00:01:00
 #SBATCH --ntasks=1
 #SBATCH --job-name=test-job
 #SBATCH --output=test-job.%j.out

 module purge
 module load python/3.5.1

 python3 test-program.py

Parametros para modulos
##############

