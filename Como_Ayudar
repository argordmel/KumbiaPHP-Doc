##################################################
COMO HACER DOCUMENTOS .RST PARA EL MANUAL
##################################################

La guía del usuario de Kumbiaphp usa Sphinx para gestionar la documentación y
salida a varios formatos. Las páginas están escritas en 
`ReStructured Text <http://sphinx.pocoo.org/rest.html>`_ format.

*************************
Códigos básicos del .rst
*************************

Todos los archivos deben terminar en .rst

* Creando un nuevo contenido

En el archivo ``source/index.rst`` ingresas el nombre del archivo de la siguiente manera

.. code-block:: php

    *********
    Categoria
    *********

    - :doc:`carpeta/archivo1`
    - :doc:`carpeta/archivo2`

Al compilarlo automáticamente tomará el título del archivo y lo indicará en el index para formar la tabla de contenido.

* Creando un título

.. code-block:: php

    ############################
    Este es un titulo de un tema
    ############################

* Creando un subtítulo

.. code-block:: php

    *******************************
    Este es un subtitulo de un tema
    *******************************

* Creando un subtítulo de 2 nivel

.. code-block:: php

    ---------------------------------
    Este es un titulo de un subtitulo
    ---------------------------------

* Escribiento en *itálica*:

.. code-block:: php

    *Hola Mundo*

* Escribiento en **negrita**:

.. code-block:: php

    **Hola Mundo**

* Resaltando una palabra o código simple. Ejemplo ``sudo service apache2 restart``

.. code-block:: php

    ``sudo service apache2 restart``

* Creando bloque de php

.. code-block:: php

    .. code-block:: php

    <?php

    class Hola extends ActiveRecord {

    }

* Creando bloque de html

.. code-block:: html

    .. code-block:: html

    <div class="row">
        <div class="col-md-6>
            <h1>Hola Mundo!</h1>
        </div>
    </div>

* Creando bloque de Javascript

.. code-block:: javascript

    .. code-block:: javascript

    (function($) {
          $(document).ready(function() {
                ... do stuff here ...
          })
     })(jQuery);

* Creando bloque de CSS

.. code-block:: css

    .. code-block:: css
    
    h1 { margin-top: 5px; }
    .example { font-size: 1.2em } 