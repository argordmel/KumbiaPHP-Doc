#############
AppController
#############

Es importante recordar que KumbiaPHP es un framework MVC y POO. En este sentido existe 
la clase **AppController** y es la súper clase de los controladores, todos deben 
heredar *extends* de esta clase para tener las propiedades (atributos) y métodos 
que facilitan la interacción entre la capa del modelo y presentación.

La clase AppController esta definida en ``app/libs/app_controller.php`` es una 
clase muy sencilla de usar y es clave dentro del MVC.

.. contents:: Contenido

***********************
Variables y/o Atributos
***********************

Cada controlador que herede de esta súper clase, heredará también sus atributos, 
de esta manera, podemos identificar el nombre del módulo, controlador, método y/o 
parámetros recibidos.

* ``$this->module_name``: Módulo actual de los controlador en ejecución
* ``$this->controller_name``: Nombre del controlador actual en ejecución
* ``$this->action_name``: Nombre del método actual en ejecución
* ``$this->parameters``: Array de datos con los parámetros recibidos para el método en ejecución

******************
Filtros y Callback
******************

Esta súper clase posee 2 filtros que se ejecutan antes y después de cada 
controlador. La estructura es la siguiente:

.. code-block:: php

    <?php
    
    class AppController extends Controller {
        
        final protected function initialize() {

        }

        final protected function finalize() {

        }
            
    }

Filtro initialize
-----------------

Este filtro se ejecuta antes de cada controlador que herede de esta súper clase. Dentro 
de sus utilidades podemos usarlas para definir un template, verificar permisos, validar 
sesiones, etc.

.. code-block:: php

    <?php
    
    class AppController extends Controller {

        final protected function initialize() {
            /**
             * Si el método de entrada es ajax, el tipo de respuesta es sólo la vista
             */
            if(Input::isAjax()) {
                View::template(NULL);
            }
        }

        final protected function initialize() {

        }
            
    }


Filtro finalize
-----------------

Este filtro se ejecuta después de cada controlador. Dentro de sus utilidades 
podemos usarlas para definir un título de página acorde a un método entre otras.

.. code-block:: php

    <?php
    
    class AppController extends Controller {

        /**
         * Titulo de la página
         */
        public $page_title = 'Página sin título';

        final protected function initialize() {

        }

        final protected function finalize() {
            //Se cambia el título de la página
            $this->page_title = trim($this->page_title).' ‹ '.APP_NAME;
        }
            
    }
