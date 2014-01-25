####################
Programación Modular
####################

Esta forma de programar hace nuestras aplicaciones mas profesionales y mantenibles en el tiempo y es que 
ahora puedes agrupar controladores por módulos con la intención de minimizar los niveles de entropía 
que se puede generar al momento de desarrollar nuestros sistemas.
   
Por lo general todos los sistemas cuentan con un modulo de usuario, donde este se debe encargar de 
realizar las tareas relacionado con el usuario podemos nombrar algunas de estas tareas son:

- Autenticar Usuarios.
- Registrar Usuarios.
- Listar Usuarios.
- Eliminar Usuarios.
- Etc.

Estas pueden ser las funcionalidades más básicas que pueden existir, de la forma como se venía haciendo 
por lo general se creaba un controlador ``usuario_controller.php`` y este se encargaba de toda esta gestión. 
Esta práctica hace que tengamos controladores muy largo y dificil de entender.

Ahora si hacemos un cambio tendremos nuestro código muchas más ordenado y es lo que propone KumbiaPHP con 
la *Programación Modular*, donde en vez de reposar todas las acciones en el mismo controlador 
tener un directorio ``controllers/usuario/`` y en este se encuentren controladores para cada acción de 
la que encarga el módulo ``usuario``.  Por ejemplo se podréa tener un controlador ``autenticar_controller.php`` 
y este tal como su nombre indica se encargaría de autenticar un usuario; otra ventaja que se nos presenta 
en este momento es que con solo ver el nombre del archivo podemos identicar de que se encarga.

Las URL's se siguen comportando de la misma manera, solo que tendremos un nivel adicional:

``http://www.example.com/usuario/autenticar/index/``

Analizando tenemos:

- *Módulo:* usuario
- *Controlador:* autenticar
- *Acción:* index


En el directorio ``views`` debemos agrupar nuestras vistas de la misma forma, siguiendo el ejemplo deberiamos tener una estructura como la siguiente:

|-- views
    |-- usuario
        |-- autenticar
                index.phml


Otro ejemplo de la programación modular, es que podemos agrupar también los controladores utilizados para los reporte:

``http://www.example.com/reporte/cliente/listar/pdf/``

- *Módulo:* reporte
- *Controlador:* cliente
- *Acción:* listar
- *Parámetro:* pdf
