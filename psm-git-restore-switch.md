Git: Los nuevos comandos git restore y git switch
Jonilson Sousa
Jonilson Sousa
12/06/2023
Git: Los nuevos comandos git restore y git switch
Por si las dudas iniciales de Git y Github no fueran suficientes, Git puede ser un tanto confuso en algunos comandos, como es el caso de git checkout. Esto no solo permite crear y cambiar entre branchs, pero también permite eliminar archivos.

Para facilitar y compartir responsabilidades, Git, a partir de la versión 2.23.0, incorpora dos nuevos comandos: el git restore y el git switch.

La confusión del git checkout
Ya tenemos un proyecto creado con el branch master y necesitamos insertar un nuevo código. Siguiendo las convenciones de desarrollo tenemos que crear una nueva branch para insertar estos cambios y luego enviarlos para su análisis y un posible merge en las master.

En este escenario el comando git checkout es nuestro gran aliado, con él podemos crear branchs usando la flag -b de esta forma:

git checkout -b nuevo-codigo
Y con esto ya creamos y seleccionamos nuestra branch llamado nuevo-codigo, siendo una gran facilidad considerando que necesitamos usar los comandos:

git branch nuevo-codigo

git checkout nuevo-codigo
Sin embargo, como ya sabes, también podemos usar git checkout para cambiar entre branch ya existentes, simplemente podemos usar el siguiente comando para volver a la branch master de nuestro proyecto:

git checkout master
Ejemplo de creación de nuevo-codigo
Además, es posible que deseemos descartar todos los cambios en el archivo index.html de nuestro proyecto, y como estábamos haciendo estos cambios en nuestro nueva branch nuevo-codigo, debemos cambiar a él y luego descartar los cambios, para eso podemos utilizar los dos comandos:

git checkout nuevo-codigo

git checkout -- index.html
alteración descartada en index.html
Bien, ahora tenemos el archivo index.htmlsin ninguna modificación, igual al estado del ultimo commit. Y áun podemos tener otras utilizaciones del comando git checkout , puedes consultar todas las posibilidades en la documentación.

Pero como podemos ver en git checkout, son muchas cosas, tenemos muchas responsabildades y eso en um momento puede confundirnos y dejarnos pensando en el uso del comando, que es bastante similar para varias acciones.

Siempre debemos ser conscientes del nivel de alcance en el que vamos a utilizar el comando git checkout. A nivel de ámbito de archivo tiene un comportamiento, a nivel de commit tiene un otro comportamiento y a nivel de branch otro comportamiento.

La división de responsabilidad
Pensando en esto, los mantenedores del Git han incorporado los nuevos comandos a partir de la versión 2.23.0 y ambos vienen con la intención de dividir responsabilidades, y de ser más específicos para las funciones que se proponen realizar.

Los nuevos comandos son git restore y git switch, veremos en las próximas sesiones con más detalles cómo funcionan estos comandos y cómo podemos ir paso a paso usándolos en lugar de usar solo git checkout.

Git restore
El git restore es una nueva opción cuando estamos trabajando y necesitamos restaurar algún archivo o el proyecto por completo , y eso es lo que git checkout también tiene, pero el git restore es especificamente para trabajar con esta parte de restauración de archivos o proyectos en un punto anterior que llamamos de fuente de restauración(source).

En nuestro proyecto que ya está siendo versionado, tenemos el archivo index.html, y ya hemos hecho tres commits:

commit 630781f424554dc271672ce75f2738095d438814
Author: ingrid <ingrid@gmail.com>
Date:   Fri Jun 02 20:56:49 2023 -0300

    Agregando barra de búsqueda

commit fa151c6535a7d0dcd1c6d792ffd2233afefa56r7
Author: ingrid <ingrid@gmail.com>
Date:   Fri Jun 02 20:47:03 2023 -0300

    Agregando el Title del sitio

commit c776f0cdefd3c6e05165feecbfe6d6a484436f16
Author: ingrid <ingrid@gmail.com>
Date:   Fri Jun 02 20:45:52 2023 -0300

    Estructura inicial de HTML5
Los dos últimos commits (Agregando el Title del sitio, Agregando barra de búsqueda) no fueran aprovados y en esto momento necesitamos volver todo el proyecto (para esto utilizamos el punto final : .) al estado del primer commit (Estructura inicial del HTML5), podemos hacerlo utilizando el git checkout informando el ID del commit de la seguinte fuerma:

git checkout c776f0cdefd3c6e05165feecbfe6d6a484436f16 .
Pero con el git restore también podemos hacer el mismo, sin embargo, debemos informar el ID del primer commit como un valor para la flag source, que es el punto o fuente de restauración de la siguiente manera:

git restore --source c776f0cdefd3c6e05165feecbfe6d6a484436f16 .
Pero podemos pensar que usando el comando git restore la sintaxe es más detallada, ahora tenemos que pasar una flag (--source) indicando qué punto, o sea, ¿qué estado queremos regresar?

La respuesta es sí, y eso es una tendencia, antes teniamos eso no solo en el Git, pero en muchas otras heramientas, esta idea de un comando realiza diversas tareas. Pero ahora los mantenedores están divididos en responsabilidad y hacen que el comando sea un poco más detallado, pero semánticamente mejor para identificar cada parte del comando, además de hacerlo más organizado y más fácil de entender para otras personas.

git switch
El git switch viene como una alternativa cuando estamos trabajando con branchs. Como git checkout podemos crear nuevas branchs y también alternar entre ellas, y con git switch podemos hacer lo mismo.

En nuestro proyecto necesitamos crear una nueva branch con el nombre nueva-branchen nuestro proyecto, podríamos usar el siguiente comando:

git switch -c nueva-branch
Ahora si ejecutamos el comando git branch para ver la lista de branchs que tenemos actualmente en el proyecto tenemos una lista como esta:

master
*nuevo-codigo
nueva-branch
Tenga en cuenta que el asterisco (*) significa qué branch está en uso en el momento, en este caso es la branch nuevo-codigo que creamos en una sesión anterior. Por lo tanto, tenemos que cambiar a esta "nueva-branch", y para eso podemos usar un comando muy similar:

git switch novo-branch
Listo, ya estamos usando la nueva-branch, para confirmamos eso podemos ejecutar el comando git branch nuevamente, esta vez, la salida debe ser con nueva-branch seleccionando:

master
nuevo-codigo
*nueva-branch
Otra posibilidad que tenemos usando el comando git switch se usa junto con el comando git branch, por lo que podríamos crear la branch con el comando git branch y simplemente seleccionar lo mismo con el interruptor:

git branch nueva-branch

git switch nueva-branch
El switch también nos proporciona un atajo muy interesante cuando necesitamos seleccionar la branch master, simplemente podemos usar un signo menos (-) en lugar del nombre de la branch:

git switch -
Si ejecutamos el comando git branch podemos ver que estamos nuevamente con la branch master seleccioanda:

*master
nuevo-codigo
nuevo-branch
Una posibilidad más que el switch disponibiliza es que cambiemos a un branch remoto , en caso un branch que nuestro proyecto no tenga localmente allí, primero debemos ejecutar el comando git feth para actualizar la información del proyecto remoto:

git fetch
Y luego usamos el comando con la siguiente sintaxis:

git switch -c <nombre-del-branch-local> --track <remoto-origin>/<nombre-del-branch-remoto>
Conclusión
Entonces podemos entender que la división de responsabilidades del comando git checkout con los comandos git restore y git switch significa que los comandos son más claros y mejor definidos.

Facilita el aprendizaje, así como la comprensión sobre las tareas que cada uno puede realizar. Y son de gran ayuda cuando estamos versionando código, ya sea en un proyecto pequeño, o en un gran proyecto de una gran empresa. Entender y saber utilizar estos nuevos recursos es muy importante. No lo sabemos con certeza, ¡pero tal vez el comando git checkout ni siquiera exista en futuras versiones de Git!

Te gustó el artículo, aquí en Alura Latam tenemos el Git y GitHub: controle y comparta su código que es un curso introductorio y también el Git y Github: estrategias de ramificación, conflictos y Pull Requests que es más avanzado y trata también del GitHub, y como usar esta poderosa herramienta en nuestro favor.

img-autor
Jonilson Sousa

Soy desarollador de software en Grupo Alura. Trabajando con las más diversas tecnologias, como Java, Python, JavaScript, PHP usando frameworks como Spring Boot, Flask. Y me gusta aprender otras tecnologías y o frameworks por diversión.

Traducido para Alura Latam por Ingrid Silva.