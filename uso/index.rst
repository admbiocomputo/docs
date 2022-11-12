.. _Uso:
**************************
Uso de los clusters asociados
**************************
Todas las tareas y los cluster asociados son gestionados con el software SLURM(Simple Linux Utility for Resources Management).

Que es SLURM?
========

`SLURM  <https://slurm.schedmd.com/overview.html>`_ es un conjunto de herramientas de software `open-source <https://www.gnu.org/philosophy/categories.html>`_ que gestiona los recursos computacionales  y agenda los trabajos en cada nodo de la federacion de clusters dedicados a la computacion cientifica en la `Universidad Nacional de Colombia <https://cecc.unal.edu.co>`_ . 

Los usuarios no ejecutan el software en estos clusters de la manera en que lo harían en una estación de trabajo:  Aqui se deben enviar los trabajos, que se ejecutan durante un tiempo definido, con  recursos  asignados, sin supervisión del usuario y con una agenda y prioridad decidida por algoritmos.

Ejecutando trabajos con Sesiones iteractivas con SLURM
***************************************************
Una sesión interactiva (o interactiva) con SLURM le posibilita reservar `recursos computacionales <https://es.wikipedia.org/wiki/Recursos_computacionales>`_  en los nodos de los clusters del CECC  para ejecutar aplicaciones  mientras se encuentra en una sesion de `shell <https://es.wikipedia.org/wiki/Shell_de_Unix>`_;  Esto permite a los usuarios ejecutar aplicaciones que requieren el control o la  decision del usuario o aplicaciones, se usa en procesos de depuracion o aplicaciones gráficas completas que requieren recursos informáticos más extensos.


En general existen 3 posibles rutas para reservar estos recursos:

- `sbatch <https://slurm.schedmd.com/sbatch.html>`_: Para enviar un  `script <https://es.wikipedia.org/wiki/Script>`_  el cual es agendado y enviado a procesar *cuando los recursos solicitados y asignados al usuario esten disponibles*; despues de enviado el usuario regresa inmediatamente a la `shell <https://es.wikipedia.org/wiki/Shell_de_Unix>`_.
- `srun <https://slurm.schedmd.com/srun.html>`_: Envio de una tarea simple, no requiere de preparacion o procesamientos posteriores. La salida de la shell--normamente la pantalla-- permite el control del usuario justo cuando el trabajo finalice.
- `salloc <https://slurm.schedmd.com/salloc.html>`_: Permite solicitar recursos sin tener necesariamente una tarea  o proceso que los use.  El usuario tendra el control de la salida estandar(Pantalla) se elimine o se cancele, la shell tambien sera bloqueada hasta que el trabajo inicie.

Que hacer y que no hacer en los Clusters
*********************************
1.  Nunca ejecute procesos en su $HOME, es un espacio de almacenamiento restringido.
2.  Siempre use el envio de procesos por lotes, exceptuando cuando usa mos nodos de la particion debug, que ejecutara maximo 3 horas y luego eliminara su proceso, aun si no ha terminado.
3.  Los nodos de login debe usarlos unicamente para editar archivos y enviar trabajos.
4.  No ejecute procesos iteractivos en los nodos de login.