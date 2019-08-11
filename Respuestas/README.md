# The Abstraction: Address Spaces #

En esta tarea aprenderemos sobre unas herramientas útiles para examinar el uso de memoria virtual de sistemas basados en Linux. 
Esto solo será una breve pista de lo que es posible; será necesario sumergirse más profundamente para convertirte verdaderamente 
en un experto (¡Como siempre!).

1. La primera herramienta que analizaremos es una herramienta muy simple, ``` free ```. Primero, abra una terminal de Linux y teclee ``` man free ```, lea su manual entero; es breve, no se preocupe! ¿Para qué sirve este comando?. Nota: Puede apoyarse en material web para entender la herramienta mediante ejemplos.

- al abrir la terminal y ejecutar este comando se muestra un manual de esta herramienta el cual presenta la siguiente descripcion: free muestra la cantidad total de memoria física y de intercambio libre y usada en el sistema, así como los búfers y cachés utilizados por el núcleo. La información se recopila analizando / proc / meminfo. Las columnas que se muestran son: total, usada(used), libre(free), compartida(shared),buffers, cache, buffers/cache y disponible(available).

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/01%20Free.png)

2. Ahora, ejecute ```free``` usando algunos argumentos que podrían ser útiles (por ejemplo, ```-m```, para mostrar 
la cantidad total de memoria en megabytes). ¿Cuánta memoria hay en su sistema?, ¿Cuánta está libre? 
¿Son estos valores los que usted esperaba?

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/02%20free%20-m.png)

3. A continuación, cree un pequeño programa que use cierta cantidad de memoria, llamado ```memory-user.c.``` Este programa debe tomar un argumento por linea de comandos: el número de megabytes de memoria que usted usará. Cuando lo ejecute, el programa debe separar memoria para un arreglo (vector) y recorrer el arreglo, accediendo consecutivamente a cada entrada (por ejemplo, escribiendo un valor inicial a cada posición). El programa deberá hacer esto indefinidamente o, por lo menos, por una cierta cantidad de tiempo especificada también por línea de comandos.

[memory-user.c](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/memory-user.c)

4. Ahora, mientras corra su programa memory-user.c, ejecute la herramienta free (en una terminal diferente, pero en la misma máquina). ¿Cómo cambia el uso total de memoria cuando su programa está corriendo?, ¿Qué pasa cuando se finaliza el programa memory-user (comando kill)?, ¿coinciden los valores con lo que usted esperaba? Intente esto para diferentes cantidades de uso de memoria. ¿Qué pasa cuando usted usa cantidades de memoria realmente grandes?.

![alt tag](https://github.com/juancr5/lab-address-spaces/blob/master/Respuestas/Imagenes/03%20memory-user.c.png)

- Si al almacenar una cantidad pequeña de mb se observa que el programa se finaliza con exito, disponiendo en memoria la cantidad de bytes ingresada por el usuario con cantidades de memoria grande el sistema operativo hace uso del swap cuando la cantidad de memoria libre es muy baja. 

- Se observa que al matar el proceso, la memoria usada y libre se restauran a los valores iniciales que se poseian antes de iniciar el proceso. Por lo tanto si los valores coincenden?; al no trabajar mucho con memoria no se posee un conocimineto absoluto de lo que deberia suceder, pero en la medida de lo evidenciado el programa se ejecuto de inmediato al hacer uso de malloc la memoria hizo un cambio de sus valores inmediatamente 
 
5. Ahora veremos una herramienta más conocida como pmap. Invierta algo de tiempo para leer el manual de pmap en detalle. ¿Cuál es la diferencia de pmap con free?


 

