##################
Redireccionamiento
##################

En un método de nuestro controlador podemos enrutar hacia otro controlador y/o acción según sea nuestro 
caso; por ejemplo, si estamos verificando o validando una información y falla, podemos direccionar a 
una acción o un controlador.

.. contents:: Contenido

*******************************
Redirección entre controladores
*******************************

.. code-block:: php

    <?php
    
    Redirect::to('controlador/');
    Redirect::to('controlador/action');
    Redirect::to('controlador/action/parameters/');


También podemos indicar el tiempo en segundos para redireccionar

.. code-block:: php

    <?php
    
    Redirect::to('controlador/', 5);
    Redirect::to('controlador/action', 10);
    Redirect::to('controlador/action/parameters/', 2);


***************************************************
Redirección entre acciones dentro de un controlador
***************************************************

.. code-block:: php

    <?php
    
    Redirect::toAction('action/');    
    Redirect::toAction('action/parameters/');


*******************
Redirección interna
*******************

Al utilizar este método KumbiaPHP lo que hace es ejecutar los parámetros indicados sin redireccionar la página. 
Este tipo de redirección es muy útil cuanto utilizas tus app con ajax.

.. code-block:: php

    <?php
    
    Redirect::route_to('module: nombre_módulo', 'controller: controlador', 'action: acción_a_ejecutar', 'parameters: parámetros_a_enviar');    


****************************************
Obteniendo información de la ruta actual
****************************************

Cuando haces un redireccionamiento, KumbiaPHP almacena las variables de la ruta actual para poder disponer de ellas en cualquier momento.

.. code-block:: php

    <?php

    //Variables que puede recibir route, module, controller, action, parameters o routed
    Router::get('var');

    $route                  = Router::get(); //Devuelve un array() con la información almacenada
    $modulo_actual          = Router::get('module');
    $controlador_actual     = Router::get('controller');
    $accion_actual          = Router::get('action');
    $parametros_recibidos   = Router::get('parameters'); //Esta opción devuelve un array() con los parámetros
    




