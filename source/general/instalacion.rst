############
Instalación
############

En esta sección, se explican los pasos a seguir, para poner a funcionar el framework en nuestro ambiente de desarrollo.

.. contents:: Contenido

**************
Requerimientos
**************

* Intérprete PHP (versión 5.2.X - 5.3.12 o superior).
* Servidor Web con soporte de reescritura de URL (Apache, Cherokee, Lighttpd, Internet Information Server (IIS)).
* Motor de base de datos soportado si se necesitase. (Ejemplo: MySQL Server, Oracle, Firebird...) 

********
Descarga
********

Para instalar KumbiaPHP Framework, se debe descargar su archivo comprimido desde la sección de 
descarga http://www.kumbiaphp.com/blog/manuales-y-descargas/ para obtener la versión más reciente del framework. 

********************************
Configurando Básica del Servidor
********************************

KumbiaPHP Framework utiliza un módulo llamado mod_rewrite para la reescritura de URLs y hacerlas más comprensibles 
y fáciles de recordar en nuestras aplicaciones. Por esto, el módulo debe ser configurado e instalado en nuestro 
servidor http. Para esto, debe chequear que el módulo esté habilitado.

----------------------
Configurando en Ubuntu
----------------------

* Activando el módulo de reescritura : ``sudo a2enmod rewrite``
* Configuración en Apache 2.4.x      : ``sudo nano /etc/apache2/apache2.conf``
* Configuración en Apache 2.2.x      : ``sudo nano /etc/apache2/sites-available/default``

Buscamos nuestro directorio y donde diga ``AllowOverride None`` y lo reemplazamos por ``AllowOverride All`` Ejemplo:

.. code-block:: php

    <Directory "/to/document/root">
        Options Indexes FollowSymLinks
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory> 

Con esto hacemos que el servidor web tenga la capacidad de leer los archivos .htaccess

* Verificamos el DirectoryIndex en Apache: ``sudo nano /etc/apache2/mods-enabled/dir.conf``

Buscamos la linea que dice ``DirectoryIndex`` y dejamos ``index.php`` en primer lugar, para que quede mas o menos asi: 

.. code-block:: php

    <IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    </IfModule>

* Reiniciamos el servidor: ``sudo service apache2 restart``
