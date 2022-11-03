# Instituto Tecnológico de Costa Rica      Principios De Sistemas Operativos
# Proyecto II                                             Grupo 50
## Elison Corrales Vargas - Ian Vargas Ledezma - Jean Carlos Urbina - Steven Alvarado Aguilar
## Programación de categorizador de páginas web utilizando el teorema de Bayes
###     El teorema de Bayes es utilizado para calcular la probabilidad de un suceso, teniendo información de antemano sobre ese suceso. Podemos calcular la probabilidad de un suceso A, sabiendo además que ese A cumple cierta característica que condiciona su probabilidad. El teorema de Bayes entiende la probabilidad de forma inversa al teorema de la probabilidad total. (J. F. López, 2021). 
###     Para la creación de este proyecto usaremos el lenguaje de programación Python y utilizaremos una base de datos en Postgresql  en ella desde Python le enviamos los diferentes urls que el programa encuentra según el código programado y busca las palabras según las clasificaciones que creamos y que más adelante vamos a explicar de mejor manera. En el proyecto implementamos las clases Bayes, Conexión, funcionespostgres y webScraping las cuáles tendrán la codificación necesaria para lograr que el proyecto cumpla con todos los requerimientos explicados por el profesor.
### Iniciamos con la clase Conexión : Esta clase se creó con la intención de tener un método de acceso a la base de datos, con esta clase podemos conectarnos a un servidor local de postgres ingresando un string de conexión. 
### Para que la conexión se realice utilizamos una librería de python llamada psycopg2 esta es un adaptador de base de datos PostgreSQL más popular para el lenguaje de programación Python. Sus principales características son la implementación completa de la especificación Python DB API 2.0 y la seguridad de subprocesos (varios subprocesos pueden compartir la misma conexión). Su instalación en el proyecto por medio de la terminal fue la siguiente: pip install psycopg2.
###     Para la clase funcionespostgres se importó la clase Conexión, ya que necesita estar en comunicación para que se conecte a la base de datos y se hagan todos los procedimientos. Primero creamos una lista con palabras. Creamos el método insertarcategoria que recibirá los parámetros nombreTabla y lista la cual abre una conexión a postgres con un cursor que tendrá el tiempo de activación en dónde iremos insertando una por una las palabras que encontraremos en una página web luego la conexión hace un commit si se llega a la última palabra, se cierra el cursor y se hace un close para cerrar la conexión con la base de datos.
### La función principal de insertarcategoria es meter las palabras que tengan que ver con una temática en específico en la base de datos, por ejemplo si se quiere realizar una base de datos que tenga palabras relacionadas a deportes el procedimiento es el siguiente:
### Buscamos en internet una página web que tenga un listado de palabras relacionadas a la temática en este caso pudimos encontrar un buen referente en el siguiente link https://relatedwords.io/sport esta pagina pide ingresar un tema y devuelve una cantidad bastante considerable de palabras relacionadas. Una vez tenemos ese listado podemos hacer uso de nuestro WebScraping para extraer estas palabras, almacenarlas en una lista y finalmente hacer uso de la función insertar categoría, de esta manera se realizó un repositorio de tablas con palabras relacionadas a una temática para preparar el teorema bayes. 
### WebScraping para sacar palabras relacionadas a una temática 
![Image text](https://github.com/IanVargas1/clasificador-bayesiano/blob/master/Picture1.png)
### Además se creó el método consultar categoría, este sirve para consultar las palabras clave de una categoría en específica, con el fin de almacenar todas las palabras clave en una estructura de datos de tal manera automatizar el hecho de no estar haciendo múltiples peticiones a la base de datos, con esta lista podemos prepararnos para el teorema bayesiano. 
![Image text](https://github.com/IanVargas1/clasificador-bayesiano/blob/master/Picture2.png)
### Creamos otro método llamado consultar no tiene ningún parámetro, debido a que una consulta donde se abre la conexión y el cursor y se ejecuta los datos de la tabla seleccionada y en la cual se va a recorrer los diferentes datos consultados y los mostraremos, luego de todo esto se cerrará tanto el cursor y la conexión. La función principal es corroborar que los elementos si se están insertando en la tabla, como un punto adicional este método podría ser dinámico de manera que podamos insertar una categoría cualquiera y devuelva el mismo resultado, en este caso únicamente consultamos la categoría deportes.
![Image text](https://github.com/IanVargas1/clasificador-bayesiano/blob/master/Picture3.png)
### Creamos el método de eliminar el cuál abrimos la conexión y el cursor ejecutamos la función de eliminar todos los datos de la base de datos, hacemos un commit para confirmar la transacción pendiente en la base de datos, esta función tiene como objetivo vaciar la tabla en la base de datos únicamente si se necesitara la reinserción en algun momento, al igual que la anterior este método podría ser genérico para poder ser utilizado con cualquier tabla.
![Image text](https://github.com/IanVargas1/clasificador-bayesiano/blob/master/Picture4.png)































