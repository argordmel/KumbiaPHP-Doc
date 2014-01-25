############
Enrutamiento
############

Por medio del ``routes.ini`` que se encuentra en la carpeta ``config`` de tu aplicativo, 
puedes definir un enrutamiento estático hacia tus controladores o acciones.

.. important:: Nota: Para utilizar el enrutamiento tienes que tenerlo activo en el archivo ``config.ini`` la línea ``routes: On``

.. contents:: Contenido

**************
Ejemplo de uso
**************

.. code-block:: php
    
    //Archivo routes.ini
    /prueba/ruta2/* = prueba/ruta3/*

Con esto indicamos que todo las peticiones que se generen para el controlador ``prueba`` y acción ``ruta2``, internamente ejecutará es el controlador ``prueba`` y acción ``ruta3``

.. code-block:: php
    
    //Archivo routes.ini
    / = home

Si en tu dominio quieres que la página principal de tu sitio no sea el ``index``, puedes indicar con el ejemplo anterior que el controlador que ejecutará para la página principal será ``home``

