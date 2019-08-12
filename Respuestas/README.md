# La Abstracción: Espacios De Direcciones #

En esta tarea aprenderemos sobre unas herramientas útiles para examinar el uso de memoria virtual de sistemas basados en Linux. 
Esto solo será una breve pista de lo que es posible; será necesario sumergirse más profundamente para convertirte verdaderamente 
en un experto (¡Como siempre!).

1. La primera herramienta que analizaremos es una herramienta muy simple, ``` free ```. Primero, abra una terminal de Linux y teclee ``` man free ```, lea su manual entero; es breve, no se preocupe! ¿Para qué sirve este comando?. Nota: Puede apoyarse en material web para entender la herramienta mediante ejemplos.

- al abrir la terminal y ejecutar este comando se muestra un manual de esta herramienta el cual presenta la siguiente descripcion: free muestra la cantidad total de memoria física y de intercambio libre y usada en el sistema, así como los búfers y cachés utilizados por el núcleo. La información se recopila analizando / proc / meminfo. Las columnas que se muestran son: total, usada(used), libre(free), compartida(shared),buffers, cache, buffers/cache y disponible(available).

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/01%20Free.png)

2. Ahora, ejecute ```free``` usando algunos argumentos que podrían ser útiles (por ejemplo, ```-m```, para mostrar 
la cantidad total de memoria en megabytes). ¿Cuánta memoria hay en su sistema?, ¿Cuánta está libre? 
¿Son estos valores los que usted esperaba?.

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/02%20free%20-m.png)

3. A continuación, cree un pequeño programa que use cierta cantidad de memoria, llamado ```memory-user.c.``` Este programa debe tomar un argumento por linea de comandos: el número de megabytes de memoria que usted usará. Cuando lo ejecute, el programa debe separar memoria para un arreglo (vector) y recorrer el arreglo, accediendo consecutivamente a cada entrada (por ejemplo, escribiendo un valor inicial a cada posición). El programa deberá hacer esto indefinidamente o, por lo menos, por una cierta cantidad de tiempo especificada también por línea de comandos.

- [memory-user.c](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/memory-user.c)
- Un ejemplo de como ejecutar el codigo es el siguiente en el cual asiganmos "memoria en mb" y despues "tiempo (segundos)" ./memory "2" "60"

4. Ahora, mientras corra su programa ```memory-user.c```, ejecute la herramienta ```free``` (en una terminal diferente, pero en la misma máquina). ¿Cómo cambia el uso total de memoria cuando su programa está corriendo?, ¿Qué pasa cuando se finaliza el programa memory-user (comando kill)?, ¿coinciden los valores con lo que usted esperaba? Intente esto para diferentes cantidades de uso de memoria. ¿Qué pasa cuando usted usa cantidades de memoria realmente grandes?.

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/03%20memory-user.c.png)

- Si al almacenar una cantidad pequeña de mb se observa que el programa se finaliza con exito, disponiendo en memoria la cantidad de bytes ingresada por el usuario con cantidades de memoria grande el sistema operativo hace uso del swap cuando la cantidad de memoria libre es muy baja. 

- Se observa que al matar el proceso, la memoria usada y libre se restauran a los valores iniciales que se poseian antes de iniciar el proceso. Por lo tanto si los valores coincenden?; al no trabajar mucho con memoria no se posee un conocimineto absoluto de lo que deberia suceder, pero en la medida de lo evidenciado el programa se ejecuto de inmediato al hacer uso de malloc la memoria hizo un cambio de sus valores inmediatamente. 
 
5. Ahora veremos una herramienta más conocida como ```pmap```. Invierta algo de tiempo para leer el manual de ```pmap``` en detalle. ¿Cuál es la diferencia de ```pmap``` con ```free```?.

- El Comando pmap reporta el mapa de la utilizacion de memoria por parte de un determinado proceso o procesos. De la infrmacion proporcionada pmap distingue entre la memoria usada por las librerias dinamicas que utiliza el proceso (columna mapped) de la que exclusivamente esta asignada a la propia aplicacion (columna writable).

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/04%20pmap%20example.jpg)

- Mientras que el comando free proporciona la informacion relativa a la cantidad de memoria fisica del sitema.

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/05%20free%20example.jpg)

6. Para usar pmap, usted tiene que conocer el identificador de proceso (PID) del proceso en el que usted está interesado. Por lo tanto, primero ejecute ```ps auxw``` para ver una lista con todos lo procesos; entonces, seleccione alguno de su interés tal como un browser. Usted también puede usar su programa memory-user en este caso (de hecho, usted puede hacer que ese programa llame a ```getpid()``` para imprimir su PID para su conveniencia).

- En este caso se uso el comando top para obtener el PID del proceso memory-user

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/06%20top.png)

- al usar pmap con el PID del proceso, este arrojo los siguintes resultados

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/06%20pmap%20memory.png)

7. Ahora ejecute ```pmap``` en alguno de estos procesos usando varias flags (como ```-X```) para revelar más detalles acerca del proceso. ¿Qué puede ver? ¿Cuántas entidades diferentes conforman un espacio de direcciones moderno, a diferencia de nuestra simple concepción de code/stack/heap?

- al hacer uso de pmap con la herramienta -x se muestra varios archivos mapeados en memoria para el proceso seleccionado y sus atributos como lo son las direcciones en memoria, sus permisos correspondientes en donde se puede evidenciar direcciones de memoria asignadas al código(archivos), asignada al heap(annon) y asignada al stack(stack)  
 
![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/07%20pmap%20-x.png)

8. Finalmente, ejecute pmap para su programa memory-user, con diferentes cantidades de memoria usada. ¿Qué puede ver en este caso? ¿La salida de pmap es siempre la que usted espera?

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/08%20procesos.png)

- Al ejecutar memory-user con 50mb  y 500mb en un tiempo de 2 minutos se observa lo siguiente: 

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/08%20memory%2050.png)

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/08%20memory%20500.png)

- Se observa que la cantidad total de memoria usada es la esperada de acuerd a la cantidad de memoria que se separa al momento de ejecutar el proceso.  

- En las diferentes ejecuciones del programa se observa que únicamente cambia  el heap, para el resto de memoria usada en cada atributo de memoria es igual para cada ejecución.

- Luego se procede a ejecutar el comando htop para observar mejor como se comporta el proceso memory-user con 500mb de memoria

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/08%20htop%20500.png)


 

