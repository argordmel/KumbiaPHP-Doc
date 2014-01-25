##########
Las Vistas
##########

Es buena práctica de desarrollo que las vistas contengan una cantidad mínima de código en PHP para 
que sea suficientemente entendible para un diseñador Web y además, para dejar a las vistas 
solo las tareas de visualizar los resultados generados por los controladores y presentar las 
capturas de datos para usuarios.

.. contents:: Contenido

******************************
Describiendo el funcionamiento
******************************

El manejador de vistas implementa el patrón de diseño de vista en dos pasos, el cual consiste en 
dividir el proceso de mostrar una vista en dos partes: la primera parte es utilizar una vista 
o *view* asociada a una acción del controlador para convertir los datos que vienen del 
modelo en lógica de presentación sin especificar ningún formato específico y la segunda es establecer el 
formato de presentación a través de una plantilla o template.

Así mismo tanto las vistas de acción como las plantillas pueden utilizar vistas parciales o partials. 
Estas vistas parciales son fragmentos de vistas que son compartidas por distintas vistas, de manera 
que constituyen lógica de presentación reutilizable en la aplicación. Ejemplos: menús, cabeceras, 
pies de página, entre otros.

KumbiaPHP favoreciendo siempre los convenios asume los siguientes respecto a las vistas:

- Todos los archivos de vistas deben tener la extensión **.phtml**.
- Cada controlador o módulo tiene un directorio de vistas asociado cuyo nombre coincide con el nombre del controlador en notación ``small_case``. Por ejemplo: si posees un controlador cuya clase se denomina ``PersonalTecnicoController`` esta por convenio tiene un directorio de vistas ``personal_tecnico``.
- Cada vez que se ejecuta una acción se intenta cargar una vista cuyo nombre es el mismo que el de la acción ejecutada.
- Los templates deben ubicarse en el directorio ``views/_shared/templates``.
- Los partials deben ubicarse en el directorio ``views/_shared/partials``.
- Por defecto se utiliza el template ``default.phtml`` para mostrar las vistas de acción

**********
Plantillas
**********

En nuestro caso, es la forma de presentación de la vista. Dentro de cada plantilla se debe 
llamar la clase y método ``View::content()`` en el lugar donde se quiera mostrar la vista así:

.. code-block:: php

    <!DOCTYPE html>
    <html lang="es">
        <head>   
            <title>Template de Ejemplo</title>     
        </head>
        <body>
            <h1>Template de Ejemplo</h1>
            <?php View::content(); ?>
        </body>
    </html>

Con ese llamado, renderizamos la vista del método del controlador en el template. 

Si es necesario cambiar el template para una acción o controlador, lo indicamos en cualquier método:

.. code-block:: php

    <?php
        
    class EjemploController extends AppController {

        protected function before_filter() {
            View::template('template_1');
        }   

        public function hola() {
            //También se puede desde cualquier método
            View::template('template_2');
        }
            
    }

Si deseas indicar un template para todos los controladores, puedes echarle un vistazo a la súper clase :doc:`AppController <app_controller>`

Si el tipo de respuesta de la vista no incluye una plantilla:

.. code-block:: php

    <?php
    
    class EjemploController extends AppController {

        public function hola() {
            if(Input::isAjax() {  //Si la petición es con Ajax se quita el template                
                View::template(NULL);
            }   
        }
            
    } 

*************************
Pasando datos al template
*************************

Para utilizar las variables de los controladores en las vistas, estas deben ser variables 
públicas **$this->nombre_variable** pues KumbiaPHP extrae esas variables y las convierte en variables 
normales **$nombre_variable**.

Ejemplo: 

.. code-block:: php

    <?php
    
    class EjemploController extends AppController {

        public $page_title = 'Título de prueba';

        public function hola() {
            View::template('mi_template');
        }
            
    } 


Template: ``view/_shared/templates/mi_template.phtml``

.. code-block:: php

    <!DOCTYPE html>
    <html lang="es">
        <head>   
            <title><?php echo $page_title; ?></title>     
        </head>
        <body>
            <h1>Template de Ejemplo</h1>
            <?php View::content(); ?>
        </body>
    </html>
 

******
Vistas
******

Como anteriormente se comentó, cada vez que se ejecuta una acción se intenta cargar una vista 
cuyo nombre es el mismo que el de la acción ejecutada.

En caso de querer cambiar el nombre de la vista que no esté asociada al nombre de la acción:

.. code-block:: php

    <?php
    
    class EjemploController extends AppController {

        public function hola() {
            View::select('saludo'); //Se cambia la vista 'hola' por defecto a 'saludo'
        }
            
    } 

En caso no querer mostrar alguna vista:

.. code-block:: php

    <?php
    
    class EjemploController extends AppController {

        public function hola() {
            View::select(NULL); //Se excluye la renderización de la vista
        }
            
    } 

************************
Pasando datos a la vista
************************

Para utilizar las variables de los controladores en las vistas, estas deben ser variables 
públicas **$this->nombre_variable** pues KumbiaPHP extrae esas variables y las convierte en variables 
normales **$nombre_variable**. 

Ejemplo: 

.. code-block:: php

    <?php
    
    class EjemploController extends AppController {

        public function hola() {
            $this->usuario = 'Mundo';
        }
            
    } 


Vista: ``view/ejemplo/hola.phtml``

.. code-block:: php

    Hola <?php echo $usuario; ?>


***********************************************
Mostrando búffer de salida de los controladores
***********************************************

Para mostrar el contenido del buffer de salida se hace uso de la clase y método **View::content()**, 
donde el contenido del búffer de salida lo constituye principalmente los mensajes
**Flash** o algunos **echo** o **print** que se hagan (se desaconseja el uso del echo o print_r 
en los controladores, pues va en contra del MVC). Al invocar **View::content()** se muestra el contenido del búffer de salida en el 
lugar donde fue invocado.

Ejemplo: 

.. code-block:: php

    <?php
    
    class EjemploController extends AppController {

        public function hola() {
            Flash::valid('Hola Mundo');
        }
            
    } 


Vista: ``view/ejemplo/hola.phtml``

.. code-block:: php

    Saludo realizado:
    <?php View::content() ?>

******************************
Indicando el tipo de respuesta
******************************

Si el tipo de respuesta es un json, pdf, xls, etc podemos indicarlo de la siguiente manera sin incluir 
el template:

Ejemplo: 


Tomemos por ejemplo esta URL:

``http://www.example.com/reporte/clientes/listar/pdf/``

.. code-block:: php

    <?php
    
    class ClienteController extends AppController {

        public function listar($formato) {
            View::response($formato);
        }
            
    } 


Tomará la siguiente vista: ``view/reporte/clientes/listar.pdf.phtml``

********
Partials
********

Los partials o vistas parciales son fragmentos de vistas que son compartidas por distintas vistas, de 
manera que constituyen lógica de presentación reutilizable en la aplicación. Por lo general los partials 
son elementos como: menús, cabecera, pie de página, formularios, entre otros.

Los partials son ubicicados en la carpeta ``views/_shared/partials/`` y lo podemos agrupar por carpetas.

Ejemplo de un partial:

.. code-block:: php

    <h1>Partial de ejemplo</h1>

Partial: ``views/_shared/partials/ejemplo.phtml``

***********************
Utilizando los partials
***********************

Para utilizar un partial se debe invocar el método ``View::partial()`` indicando como argumento el partial 
deseado y la vista parcial se mostrará en el lugar donde se invocó.

Ejemplo: 

.. code-block:: php

    <!DOCTYPE html>
    <html lang="es">
        <head>   
            <title>Template de Ejemplo</title>   
        </head>
        <body>
            <h1>Template de Ejemplo</h1>

            <?php View::partial('ejemplo'); ?>

            <?php View::content(); ?>
        </body>
    </html>


Cabe destacar que los partial se pueden utilizar tanto en vistas de acción, templates e incluso dentro de otros partials.

****************************
Pasando datos a los partials
****************************

Para pasar datos a un partial, estos se deben indicar en un array asociativo donde cada clave con su 
correspondiente valor se cargarán como variables en el ámbito local del partial.

Ejemplo: 

.. code-block:: php

    <h1>Usuario: <?php echo $usuario ?></h1>

Partial: ``view/_shared/partials/usuario.phtml``

.. code-block:: php

    <?php View::partial('usuario', FALSE, array('usuario' => 'Ejemplo')) ?>
    
    <p>Este es un ejemplo </p>

Vista: ``views/ejemplo/prueba.phtml``
