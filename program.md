
# (PART) Programar {-}

# Introducción {#programar-intro}

En esta parte del libro, mejorarás tus aptitudes de programación. La programación es una habilidad que cruza transversalmente todos los trabajos de ciencia de datos: deberás usar una computadora para hacer ciencia de datos, no puedes hacerlo sólo con tu cabeza o con lápiz y papel.

<img src="diagrams/data-science-program.svg" width="75%" style="display: block; margin: auto;" />

Programar produce código, y el código es una herramienta de comunicación. Obviamente el código le dice a la computadora qué es lo que quieres que haga, pero también comunica el significado a otros humanos. Es importante pensar el código como un medio de comunicación, porque todo proyecto que realices es esencialmente colaborativo.  Aún cuando no estés trabajando con otras personas, seguramente en el futuro trabajarás con ese mismo código.  Por eso es necesario escribir código claro, para que otros (o tú en el futuro) puedan entender por qué encaraste un análisis de la manera que lo hiciste. Esto significa que mejorando la programación también mejorarás la comunicación. Pasado el tiempo, querrás que tu código resulte no solo fácil de escribir, sino también fácil de leer para otros.     

Escribir código es similar,  en muchas formas, a escribir prosa. Un paralelismo que encuentro particularmente útil es que en ambos casos reescribir es clave para la claridad. La primera expresión de tus ideas difícilmente sea clara, y posiblemente necesitarás reescribir muchas veces. Después de resolver el problema de análisis de datos, en general es mejor mirar tu código y pensar si es obvio o no lo que has hecho.  Si utilizas un poco de tiempo reescribiendo tu código mientras las ideas están frescas, puedes ganar mucho tiempo después, cuando necesites recrear el código que hiciste. Esto no significa que debas reescribir todas las funciones: necesitas equilibrar qué es lo que tienes que mejorar ahora para ganar tiempo a largo plazo. (Pero cuanto más reescribas tus funciones, más probable será que tu primer intento sea cada vez más claro).

En los próximos cuatro capítulos, aprenderás habilidades que te permitirán abordar nuevos programas como también resolver problemas ya existentes de manera más sencilla y con mayor claridad: 

1.  En [_pipes_], navegarás dentro del __pipe__, `%>%`, y aprenderás más sobre cómo trabaja, qué alternativas existen y cuándo no conviene usarlo.

2.  Copiar y pegar (_copy-and-paste_) es muy práctico, pero deberías evitar usarlo más de dos veces. Repetir el código dentro de un programa es peligroso porque puede llevar a errores e inconsistencias. Por eso, en [funciones], aprenderás a escribir __funciones__ que permiten extraer código repertido y convertirlo en código fácilmente reutilizable.

3.  A medida que comiences a escribir funciones más potentes, necesitarás una base sólida en las __estructuras de datos__ de R, que te proporcionará [vectores]. Deberás dominar los cuatro tipos de vectores atómicos clásicos, también las tres clases S3 construídas sobre ellos, y entender los misterios de las listas y los _data frame_. 

4.  Las funciones previenen que repitamos código, pero muchas veces necesitas repertir las mismas acciones con diferentes entradas. Necesitas, entonces, herramientas de __iteración__ que te permitan hacer cosas similares una y otra vez. Estas herramientas incluyen ciclos (_loops_) y programación funcional que aprenderás en [iteración].

## Aprendiendo más

El objetivo de estos capítulos es enseñarte lo básico de programación que necesitas para hacer ciencia de datos, que resulta una cantidad considerable de información. Una vez que hayas dominado el material de este libro, creo firmemente que deberías  invertir tiempo en mejorar tus habilidades de programación. Aprender más sobre programación es una inversión a largo plazo: no obtendrás resultados inmediatos, pero con el tiempo te permitirá resolver nuevos problemas más rápidamente, y te permitirá reutilizar tus ideas de problemas anteriores en nuevos escenarios.

Para profundizar necesitas estudiar R como un lenguaje de programación, no sólo como un ambiente interactivo para ciencia de datos. Escribimos dos libros que te ayudarán en ese sentido. Estos libros sólo están disponibles en inglés:

* [_Hands on Programming with R_](https://amzn.com/1449359019), 
  por Garrett Grolemund. Ésta es una introducción a R como lenguaje de programación 
  y es un buen lugar para empezar si R es tu primer lenguaje de programación. Cubre 
  casi el mismo material que estos capítulos, pero con un estilo diferente y con
  distintos ejemplos de motivación (basados en el casino). Es un complemento muy útil 
  si consideras que estos cuatros capítulos van demasiado rápido.
  
* [_Advanced R_](https://amzn.com/1466586966) por Hadley Wickham. Este libro bucea en los 
  detalles del lenguaje de programación R. Éste es un buen punto por donde empezar si
  ya tienes experiencia en programación. Es también una buena manera de seguir una vez que  
  hayas internalizado las ideas de estos cuatro capítulos. Puedes leerlo online en el sitio
  <http://adv-r.had.co.nz>.
 
