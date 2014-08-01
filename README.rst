##################################################
Bienvenido a la guía de inicio rápido de KumbiaPHP
##################################################

*********************************
Manual para la versión 1.0 Spirit
*********************************

`Guía de inicio </source/index.rst>`_.

*********************************
Convertir a html
*********************************

La guía del usuario de Kumbiaphp usa Sphinx para gestionar la documentación y
salida a varios formatos. Las páginas están escritas en 
`ReStructured Text <http://sphinx.pocoo.org/rest.html>`_ format.

Instalación
===========

1. ``sudo apt-get install python-setuptools``
2. ``sudo easy_install sphinx``
3. ``sudo easy_install sphinxcontrib-phpdomain``
4. ``cd Kumbiaphp-Doc``
5. ``make html``

Una vez se ha compilado se creará una carpeta llamada ``build`` que contiene los archivos html