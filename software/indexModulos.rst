.. _indexModulos
**Sistema de Modulos**
****************

La mayoria del software no se encuentra en el sistema operativo las rutinas que logran ubicar el software y sus dependencias son gestionadas por los módulos que permiten tener varias versiones de manera concurrente o permitir cambiar entre ellas de modo facil.


Comando `module`
##########

Los modulos  pueden ser llamados por los scripts con los que se envia un trabajo o en una sesion iteractiva.  Existen algunos comando que puede usar en los modulos. 

Para ver los modulos disponible ejecute en una terminal o consola:

``
module avail
``

Esto retornara una lista de modulos que puede carga en su ambiente.

Para cargar el modulo que eligio en su ambiente ejecute:

```bash
module load some_module

# ej: "module load python"
```

You can specify the version of the software by appending a `/` with
the version number:

```bash
module load some_module/version 

# example: "module load python/3.5.1"
```

The Lmod hierarchical module system provides five layers to support
programs built with compiler and library consistency requirements. A
module’s dependencies must be loaded before the module can be loaded.

The Layers include:

+ Independent programs
+ Compilers
+ Compiler dependent programs
+ MPI implementations
+ MPI dependent programs 

If you cannot load a module because of dependencies, you can use the
`module spider` to find what dependencies you need to load the module.

```bash
module spider some_module

# example: "module spider openmpi"
```

### Loading Modules in a Job Script

Loading a module will enable access to the modules 
described software package. Additionally, modules 
will set or modify a user’s environment
variables.

Modules in a job script can be loaded after your `#SBATCH` directives
and before your actual executable is called. A sample job script that
loads Python into the environment is provided below:

```bash
#!bin/bash
#SBATCH --nodes=1
#SBATCH --time=00:01:00
#SBATCH --ntasks=1
#SBATCH --job-name=test-job
#SBATCH --output=test-job.%j.out

module purge
module load python/3.5.1

python3 test-program.py
```

### Subcommands

The `module` command has a variety of subcommands, outlined in the
table below. You may shorten the command to `ml`, but the shortened
command may require specialized syntax.

Command                 | Shortened Command            | Description  | Example |
----------------------- | ---------------------------- | ------------ | --------|
`module avail`          | `ml av`                      | List available software. Modules not listed here may have unmet dependencies which must be loaded for the module to be available. | `module avail`
`module spider <module>`| `ml spider <module>`         | Searches for a particular software. | `module spider openmpi`
`module load <module>`  | `ml <module>`                | Load a module to use the software. In this example we are loading the GNU Compiler Collection. The default version will load because we have not specified a version. | `module load gcc`
`module load <module>/<version>` | `ml <module>/<version>`      | Load GCC version 6.1.0 | `module load gcc/6.1.0`
`module unload <module>`     | `ml -<module>`               | Remove or unload a module | `module unload gcc`
`module swap <module> <new_module>` | `ml -<module> <new_module>`  | Swap a module. In this example we are unloading GCC and loading Intel. Any GCC-dependent modules will also be unloaded, and the intel-dependent versions (if available) will be loaded in their place. | `module swap gcc intel`
`module purge`          | `ml purge`                   | Remove all modules. The `slurm` module will not be unloaded with this purge because it is sticky. Use the `--force` flag to unload a sticky module. | `module purge`
`module save <name>`       | `ml save <name>`            | Save the state of all loaded modules. In this example, we are saving all loaded modules as a collection called `foo` | `module save foo`
`module restore <name>`    | `ml restore <name>`  | Restore a state of saved modules. In this example, we are restoring all modules that were saved as the collection called `foo` | `module restore foo`
`module help`           |                   | Find information about additional module sub-commands. | `module help`
