Si deseas verificar el historial de cambios, los mensajes de commit, el nombre de la persona autora del commit y otras informaciones sobre el proyecto, hay un comando de git que te puede ayudar. Este comando es git log.

Como ya sabemos, los commits poseen hashs que los identifican de una manera única, es decir, no existen dos commits con el mismo hash. Con git log podemos ver el hash y muchas otras informaciones del commit.

Podemos visualizar todos los commits, uno en cada línea con el comando:

git log –oneline
COPIA EL CÓDIGO
Si, en lugar de menos informaciones, queremos ver más, como las alteraciones del commit, podemos usar:

git log -p
COPIA EL CÓDIGO
También podemos buscar las informaciones de la persona autora del commit con el comando:

git log --author="user_name"
COPIA EL CÓDIGO
Y buscar informaciones por fecha:

git log --since=1.month.ago --until=1.day.ago
COPIA EL CÓDIGO
En el comando anterior, estamos buscando las informaciones del commit desde hace un mes hasta hace un día.

Tu también puedes formatear la visualización de las informaciones del commit con el comando:

git log --pretty="format:%h %s"
COPIA EL CÓDIGO
Esto trae el hash seguido del mensaje de commit. Para saber más formas de mostrar las informaciones del commit, aquí hay una lista de formas en que puedes hacer https://devhints.io/git-log-format

Genial, ¿no? ¿Qué pasaría si te dijeras que hay muchos otros parámetros que podemos pasar en git log? Si deseas saber más sobre cómo mostrar tu información de commit, puedes consultar a este https://devhints.io/git-log