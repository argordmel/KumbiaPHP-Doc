###########
Los Modelos
###########

Los modelos son la lógica de negocio y todo lo que tiene que ver con el acceso a la base de datos. 
Los modelos son ubicados dentro de la carpeta **models** de nuestra aplicación.

.. contents:: Contenido

***************************
Convenciones en los modelos
***************************

Como convención los archivos se deben llamar igual que el nombre de la tabla; ejemplo: **cliente.php**, 
**tipo_cliente.php**.  De igual manera en la base de datos las llaves primarias se deben llamar **id** y 
deben ser AUTOINCREMENT o SERIAL.

Los campos terminados en ***_id** se utilizan para relaciones foráneas a otras tablas. Ejemplo 
**libro_id** indica que posee una relación con la tabla **libro**.

Si se desea almacenar la fecha de registro y modificación se pueden crear los campos ***_at** para el 
registro y **_in** para la modificación. Ejemplo: cliente_at, cliente_in. Adicionalmente deben 
ser tipo DATETIME, el cual KumbiaPHP cargará el valor automáticamente.

*********************
Como usar los Modelos
*********************

Los Modelos representan la lógica de la aplicación y son parte fundamental para el momento que se desarrolla 
una aplicación, un buen uso de estos nos proporciona un gran poder al momento que se necesita escalar, 
mantener y reusar código en una aplicación. Por lo general un mal uso de los modelos es solo dejar el 
archivo con la declaración de la clase y toda la lógica se genera en el controlador. Esta práctica trae 
como consecuencia que en primer lugar el controlador sea dificilmente entendible por alguien que intente 
agregar y/o modificar algo en esa funcionalidad, en segundo lugar lo poco que puedes rehusar el código en 
otros controladores y lo que hace es repetirse el código que hace lo mismo en otro controlador. Partiendo 
de este principio los controladores NO deberían contener ningún tipo de lógica solo se encargan de atender 
las peticiones del usuarios y solicitar dicha información a los modelos, con esto garantizamos un buen uso 
del MVC.

********************
Definiendo un Modelo
********************

La clase de cada modelo se debe llamar de la siguiente manera:

.. code-block:: php

    <?php
    
    class TipoCliente extends ActiveRecord {
            
    }

*********************************************
Invocando un modelo en nuestros controladores
*********************************************

En KumbiaPHP existen 2 formas de invocar nuestros modelos según nuestros casos requeridos

- ``Load::models('nombre_modelo', 'nombre_otro_modelo');`` 
    De esta manera incluimos el (los) archivo(s) correspondiente(s) al (los) modelo(s) indicados(s).  Esta 
    metodología es útil si necesitamos utilizar el modelo en más de una acción dentro de uno o varios 
    controladores.    
- ``Load::model('nombre_modelo');`` 
    De esta manera devuelve un objeto creado del modelo indicado.  Esta metodología es útil cuando solo 
    hacemos uso de un modelo en un solo método o acción dentro de un controlador.
    

Veamos el siguiente ejemplo:

.. code-block:: php

    <?php

    //Cargamos los modelos sin la extensión .php para usarlo en cualquier método
    Load::models('cliente', 'tipo_cliente');

    class ClienteController extends AppController {
            
        /**
         * Método para ver la información del cliente
         */
        public function ver($id) {
            
            $cliente = new Cliente();
            $cliente = $clientes->find_first((int)$id);

            //Cargo el modelo compra sólo para usarlo en este método
            $compras = Load::model('compra')->find("cliente_id = $cliente->id");
            
            //Se almacenan lo resultados en variables públicas para utilizarlas en la vista
            $this->cliente = $cliente;
            $this->compras = $compras;
        }

    }
