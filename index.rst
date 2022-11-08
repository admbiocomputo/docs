.. HPC-CECC documentation master file, created by
   sphinx-quickstart on Tue Sep 20 00:19:10 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Bienvenido al HPC del  CECC!
=================

Este sitio contiene la documentacion de la Federacion de clusters del Centro de Excelencia para Computacion Cientifica de la Universidad Nacional de Colombia  `"CECC" <https://cecc.unal.edu.co/>`_

.. image:: /images/DiagramHPC.svg
    :width: 780px
    :align: center
    :height: 560px
    :alt: Estructura CECC

Obtener Acceso
=========

El Director del grupo de Investigacion de la Universidad Nacional de Colombia aplicara para un proyecto en `URL <https://cecc.unal.edu.co/solicitud_proyecto />`_  y el sera quien solicite  para usted el ingreso, luego de asignados los recursos, usted  recibira un correo informando su Usuario/Password.

Iniciar sesión en el HPC del CECC
===================

La federacion de clusters del CECC usa un cortafuegos que aisla el sistema de la Internet y solo usuarios e IPs incluidas de una lista permitida pueden acceder. 

Antes de que pueda iniciar sesión en el HPC, debe establecer una contraseña y aceptar las normas de uso acerca de la administracion de identidad  publicadas en el Portal `URL <https://cecc.unal.edu.co/solicitud_proyecto />`_  haciendo uso de la cuenta y  contraseña que sera entregada al Director del grupo de Investigacion y proyecto.

El cortafuegos del HPC solo permite conexiones SSH entrantes, ssh o scp del HPC a otros nodos externos al campus está deshabilitado y se debera ser solicitado por parte del Director del grupo de investigacion en  `URL <https://cecc.unal.edu.co/solicitud_proyecto />`_. 

La Federacion de Cluster del CECC usa nodos de inicio de sesión para el acceso interactivo y para el envío de trabajos por lotes. 

Hardware de la Federacion de Clusters del CECC
============================

Cluster biocomputo, 7Nodos, 120Threads, 334Gb RAM
*************************************************

.. csv-table::  7Nodos, 120Threads, 334Gb RAM 
   :header: "nodo", "Hercules1", "Hercules2", "Hercules3", "Hercules4", "Hercules5", "hercules6", "hercules7"
   :widths: 27, 30, 30, 30, 30, 30, 30, 30

   "Procesador", "Xeon E5620", "Xeon E5620", "Xeon E5620",  "Xeon E5620", "Xeon E5620", "Xeon E5-2609", "Xeon Silver 4208"
   "Slots/Nodo", "2", "2", "2", "2", "2", "2", "2"
   "Cores/Nodo", "8", "8", "8", "8", "8", "4", "16"
   "Threads/Nodo", "16", "16", "16", "16", "16", "8", "32"
   "Velocidad Turbo", "2.66 GHz", "2.66 GHz", "2.66 GHz", "2.66 GHz", "2.66 GHz", "2.50 GHz", "3,20 GHz" 
   "RAM/Nodo", "22Gb\@0.9 ns", "47Gb\@0.9 ns", "47Gb\@0.9 ns", "47Gb\@0.9 ns", "47Gb\@0.9 ns", "62Gb\@0.6 ns", "62Gb\@0.3 ns"
   
			
Cluster qTeorica,
***************						

     "Velocidad Base", "2.40 GHz", "2.40 GHz", "2.40 GHz", "2.40 GHz", "2.40 GHz", "2.50 GHz", "2,10 GHz"
 
   
   
  


+------------+--------------+-------------+---+--+----+---+--+
| Header 1   | Header 2   | Header 3  |4   |   5|   6 | 7   | 8 |
+======+======+======+=+=+==+=+=+
| row 1 | column 2   | column 3  |4 | 5| 6 | 7 | 8 |
+------------+--------------+-------------+---+--+----+---+--+



.. toctree::
   :maxdepth: -1
   :hidden:
   
  ingreso.rst
  asociados/index.rst
  software/index.rst
  uso/index.rst
  


Indices y tablas
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
