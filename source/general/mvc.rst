############################################
Arquitectura MVC (Model - View - Controller)
############################################

En 1979, Trygve Reenskaug desarrolló una arquitectura para desarrollar aplicaciones interactivas. 
En este diseño existían tres partes: modelos, vistas y controladores. El modelo MVC permite hacer la 
separación de las capas de interfaz, modelo y lógica de control de ésta. La programación por capas, 
es un estilo de programación en la que el objetivo primordial es la separación de la lógica de negocios 
de la lógica de diseño, un ejemplo básico de esto es separar la capa de datos de la capa de presentación al 
usuario.

*********************
Qué es un Controlador
*********************

El Controlador es el objeto que proporciona significado a las órdenes del usuario, actuando sobre los 
datos representados por el Modelo. Cuando se realiza algún cambio, entra en acción, bien sea por 
cambios en la información del Modelo o por alteraciones de la Vista.

****************
Qué es un Modelo
****************

Es la lógica de negocio de un aplicativo. El Modelo no tiene conocimiento específico de los 
Controladores o de las Vistas, ni siquiera contiene referencias a ellos. Es el propio sistema el que 
tiene encomendada la responsabilidad de mantener enlaces entre el Modelo y las Vistas.

****************
Qué es una Vista
****************

La Vista es el objeto que maneja la presentación visual de los datos representados por el Modelo 
y que son mostrados al usuario. Una vista puede ser un archivo html, xml, pdf, csv, odt, doc, xls, etc.

******************
Resumiendo un poco
******************

En una aplicación web la vista es la página HTML y/o todo lo que el usuario pueda ver en la pantalla. 
El controlador es el código que provee de datos dinámicos a la página y da respuestas al usuario. 
El modelo es el Sistema de Gestión de Base de Datos y/o la Lógica de negocio.

*********************
Analizando un ejemplo
*********************

Todos hemos visto un tablero de ajedrez, ahora analicemos un poco ese juego.

El tablero y las fichas son la vista (lo que el jugador puede ver). Cada ficha cumple cierta regla 
y su movimiento depende de ella, esto lo defino como el modelo. El controlador es el que se encarga 
de mover cada ficha y colocarla en un cuadro del tablero dependiendo de la estrategia del juego. Es un 
ejemplo sencillo pero podemos comprender mejor el funcionamento de esta arquitectura.

*************************************
Por qué KumbiaPHP aplica este patrón?
*************************************

El objetivo de este patrón es el realizar y mantener la separación entre la lógica de nuestra 
aplicación, los datos y la presentación. Esta separación tiene algunas ventajas importantes, como 
poder identificar más fácilmente en qué capa se está produciendo un problema con sólo conocer su naturaleza. 
Podemos crear varias presentaciones sin necesidad de escribir varias veces la misma lógica de aplicación. Cada 
parte funciona independiente y cualquier cambio centraliza el efecto sobre las demás, así que podemos 
estar seguros que una modificación en un componente realizará bien las tareas en cualquier parte de la aplicación.
