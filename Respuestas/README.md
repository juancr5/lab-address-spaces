# The Abstraction: Address Spaces #

En esta tarea aprenderemos sobre unas herramientas útiles para examinar el uso de memoria virtual de sistemas basados en Linux. 
Esto solo será una breve pista de lo que es posible; será necesario sumergirse más profundamente para convertirte verdaderamente 
en un experto (¡Como siempre!).

## Antes de empezar ##

Para responder a las preguntas lea y reflexione sobre el capítulo [The Abstraction: Address Spaces]( http://pages.cs.wisc.edu/~remzi/OSTEP/vm-intro.pdf) pues de este fue del que se sacaron las preguntas. Adicionalmente entienda y ejecute el código asociado a dicho capítulo el cual se encuentra en el siguiente [enlace](https://github.com/remzi-arpacidusseau/ostep-code/tree/master/vm-intro). 

Adicionalmente, donde crea que sea necesario haga uso de los conceptos sobre procesos aprendidos en el laboratorio anterior.

## Preguntas ##

1. La primera herramienta que analizaremos es una herramienta muy simple, ```free```. Primero, abra una terminal de Linux y 
teclee ```man free```, lea su manual entero; es breve, no se preocupe! ¿Para qué sirve este comando?. **Nota**: Puede apoyarse en 
material web para entender la herramienta mediante ejemplos.

2. Ahora, ejecute ```free``` usando algunos argumentos que podrían ser útiles (por ejemplo, ```-m```, para mostrar 
la cantidad total de memoria en megabytes). ¿Cuánta memoria hay en su sistema?, ¿Cuánta está libre? 
¿Son estos valores los que usted esperaba?



## Referencias ##

1. http://u.cs.biu.ac.il/~linraz/os/OS3.pdf
2. https://www.ostechnix.com/run-command-specific-time-linux/
3. http://u.cs.biu.ac.il/~linraz/os/OS4.pdf
4. http://u.cs.biu.ac.il/~linraz/os/OS5.pdf
