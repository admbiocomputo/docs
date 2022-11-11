
Autentificacion con Clave Publica
===================

La razon para usar dos claves --o llaves-- separadas en lugar de una contrasena simple es la seguridad.

ssh usa algoritmos que generan un par de llaves especificas para cada usuario:  una llave publica y una llave privada.   La clave o llave publica se copia en el servidor y cualquiera que tenga una copia de la clave publica puede cifrar(encriptar) los datos, que luego solo pueden ser leidos--descifrados--por quien posee la clave privada.

Una vez que un servidor SSH recibe una clave pública de un usuario y considera que la clave es confiable, el servidor registra la clave como autorizada en el archivo authorized_keys. Estas claves se denominan claves autorizadas.

La clave privada que permanece "unicamente" con el usuario es prueba de la identidad del usuario.  Solo el usuario que posea la  clave privada que corresponda a la clave pública en el servidor podrá autenticarse con éxito.

Las claves privadas deben almacenarse y administrarse con cuidado,  NO se deben distribuir copias de la clave privada. Las claves privadas utilizadas para la autenticación de usuarios se denominan claves de identidad.

Los Siguiente pasos muestras los pasos para autentificar con Clave Publica:

1.  Crear el par de claves desde  una consola con ssh-keygen

2.  La clave privada DEBE permanecer con el usuario o segura en la maquina desde donde se realice la coneccion, la clave publica se envia al servidor y debe ser almacenada como autorizada.

El servidor ahora permitirá el acceso a cualquier persona que pueda demostrar que tiene la clave privada correspondiente.


