
# (PARTE) Domar datos {-}


# Introducción {#domar datos -intro}

En esta parte del libro, aprenderás cómo domar datos: el arte de tener tus datos en R de una forma conveniente para su visualización y modelado. La doma de datos es muy importante: ¡sin ella no puedes trabajar con tus propios datos! Existen tres partes principales para la doma de datos:  

<img src="diagrams/data-science-wrangle.svg" width="75%" style="display: block; margin: auto;" />

Esta parte del libro continúa de la siguiente forma:

*   En [tibbles], aprenderás sobre la variante de _data frame_ que usamos
    en este libro: el __tibble__.  Conocerás qué los hace diferentes de los
    data frames comunes, y cómo puedes construirlos "a mano".

*   En [importar datos], aprenderás cómo traer tus datos del disco y dejarlos en R.
    Nos enfocaremos en los formatos rectangulares de texto plano, pero daremos referencias  
    a paquetes que ayudan con otros tipos de datos.

*   En [datos ordenados], aprenderás una manera consistente de almacenar
    tus datos que facilita la transformación, la visualización y el modelado de los mismos.
    Aprenderás los principios subyacentes, y cómo poner tus datos en una forma ordenada.

La doma de datos también abarca la transformación de los mismos, sobre lo cual ya has aprendido un poco. Ahora nos enfocaremos en nuevas habilidades para tres tipos de datos específicos que encontrarás frecuentemente en la práctica:

*   Los [datos relacionales] te darán herramientas para trabajar con múltiples
    conjuntos de datos interrelacionados.
    
*   Las [cadenas de caracteres] te introducirán en las expresiones regulares (_regular expressions_), las cuales son una herramienta 
    poderosa para manipular cadenas de caracteres.

*   Los [Factores] indican cómo R almacena los datos categóricos. Se usan cuando una variable
    tiene un conjunto fijo de posibles valores, o cuando quieres usar una cadena de caracteres en un 
    orden distinto al alfabético.
    
*   Las [Fechas y horas] te darán herramientas clave para trabajar con  
    fechas y fecha-horas.
