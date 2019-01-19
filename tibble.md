
# Tibbles

## Introducción


A lo largo de este libro, trabajaremos con "tibbles" (pronunciado /tibl/) en lugar de los tradicionales `data.frame`s de R. Los tibbles __son__ __data frames__, que modifican algunas características antiguas para hacernos la vida más fácil. R es un lenguaje viejo y algunas cosas que eran útiles hace 10 o 20 años, actualmente pueden resultar inconvenientes. Es difícil modificar R base sin alterar el código existente, así que la mayor parte de la innovación ocurre en paquetes. Aquí describiremos el paquete __tibble__, que provee data frames prácticos que facilitan el trabajo con el tidyverse. La mayoría de las veces voy a usar el término tibble y data frame de manera indistinta; para referirme al data frame de R lo voy a llamar `data.frame`.

Si luego de leer este capítulo te quedas con ganas de aprender más sobre tibbles, quizás disfrutes `vignette("tibble")`.

### Requisitos

En este capítulo exploraré el paquete __tibble__, parte de los paquetes principales del tidyverse.


```r
library(tidyverse)
```

## Creando tibbles {#tibbles}

La mayoría de las funciones que usarás en este libro producen tibbles, ya que éstos son una de las características principales de tidyverse. La mayoría de los paquetes de R suelen usar data frames clásicos, así que quizás quieras convertir un data frame en un tibble. Esto lo puedes hacer con `as_tibble()`:


```r
as_tibble(iris)
#> # A tibble: 150 x 5
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <fct>  
#> 1          5.1         3.5          1.4         0.2 setosa 
#> 2          4.9         3            1.4         0.2 setosa 
#> 3          4.7         3.2          1.3         0.2 setosa 
#> 4          4.6         3.1          1.5         0.2 setosa 
#> 5          5           3.6          1.4         0.2 setosa 
#> 6          5.4         3.9          1.7         0.4 setosa 
#> # … with 144 more rows
```

Puedes crear un nuevo tibble a partir de vectores individuales con `tibble()`. Esta función recicla vectores de longitud 1 automáticamente y te permite usar variables creadas dentro de la propia función, como se muestra abajo.


```r
tibble(
  x = 1:5,
  y = 1,
  z = x^2 + y
)
#> # A tibble: 5 x 3
#>       x     y     z
#>   <int> <dbl> <dbl>
#> 1     1     1     2
#> 2     2     1     5
#> 3     3     1    10
#> 4     4     1    17
#> 5     5     1    26
```

Si ya estás familiarizado con `data.frame()`, es importante que tomes en cuenta que `tibble()` hace menos cosas: nunca cambia el tipo de los inputs (p.e. ¡nunca convierte caracteres en factores!), nunca cambia el nombre de las variables, y nunca asigna nombres a las filas.

Un tibble puede usar nombres de columnas que no son nombres de variables válidos en R; es decir nombres __no sintácticos__. Por ejemplo, pueden empezar con un caracter diferente a una letra, o contener caracteres poco comunes, como espacios. Para referirse a estas variables, tienes que rodearlos de acentos graves, `` ` ``:


```r
tb <- tibble(
  `:)` = "sonrisa", 
  ` ` = "espacio",
  `2000` = "número"
)
tb
#> # A tibble: 1 x 3
#>   `:)`    ` `     `2000`
#>   <chr>   <chr>   <chr> 
#> 1 sonrisa espacio número
```

También necesitarás los espacios abiertos al trabajar con estas variables en otros paquetes, como ggplot2, dplyr y tidyr.

Otra forma de crear un tibble es con `tribble()`, que es una abreviación de tibble **tr**anspuesto. Esta función está pensada para realizar la entrada de datos en el código: los nombres de las columnas se definen con fórmulas (comienzan con `~`), y cada entrada está separada por comas. Esto permite escribir pocos datos de manera legible.



```r
tribble(
  ~ x, ~ y, ~ z,
  #--|--|----
  "a", 2, 3.6,
  "b", 1, 8.5
)
#> # A tibble: 2 x 3
#>   x         y     z
#>   <chr> <dbl> <dbl>
#> 1 a         2   3.6
#> 2 b         1   8.5
```

Usualmente agrego un comentario para dejar en claro cuál es el encabezado (esta línea debe empezar con `#`).

## Tibbles vs. data.frame

Existen dos diferencias principales entre el uso de un tibble y un `data.frame` clásico: la impresión en la consola y la selección de los subconjuntos.

### Impresión en la consola

Los tibbles tienen un método de impresión en la consola refinado: sólo muestran las primeras 10 filas, y sólo aquellas columnas que entran en el ancho de la pantalla. Esto simplifica y facilita trabajar con bases de datos grandes. Además del nombre, cada columna muestra su tipo. Esto último es una característica útil tomada de `str()`.


```r
tibble(
  a = lubridate::now() + runif(1e3) * 86400,
  b = lubridate::today() + runif(1e3) * 30,
  c = 1:1e3,
  d = runif(1e3),
  e = sample(letters, 1e3, replace = TRUE)
)
#> # A tibble: 1,000 x 5
#>   a                   b              c     d e    
#>   <dttm>              <date>     <int> <dbl> <chr>
#> 1 2019-01-19 20:43:09 2019-01-26     1 0.368 h    
#> 2 2019-01-20 14:48:19 2019-01-31     2 0.612 n    
#> 3 2019-01-20 09:11:58 2019-02-10     3 0.415 l    
#> 4 2019-01-19 22:33:15 2019-02-09     4 0.212 x    
#> 5 2019-01-19 18:57:32 2019-02-06     5 0.733 a    
#> 6 2019-01-20 05:58:29 2019-02-02     6 0.460 v    
#> # … with 994 more rows
```

Los tibbles están diseñados para no inundar tu consola accidentalmente al mirar data frames muy grandes. Sin embargo, a veces es necesario un output mayor que el que se obtiene por default. Existen algunas opciones que pueden ayudar. 

Primero, puedes usar `print()` en el data frame y controlar el número de filas (`n`) y el ancho (`width`) mostrado. Por otro lado, `width = Inf` muestra todas las columnas:


```r
vuelos %>% 
  print(n = 10, width = Inf)
```

También puedes controlar las características de impresión, modificando las opciones que estan determinadas por default.

* `options(tibble.print_max = n, tibble.print_min = m)`: si hay más de `n` filas, mostrar solo `m` filas. Usa `options(tibble.print_min = Inf)` para mostrar siempre todas las filas.

* Usa `options(tibble.width = Inf)` para mostrar siempre todas las columnas sin importar el ancho de la pantalla.

Puedes ver una lista completa de opciones en la ayuda del paquete con `package?tibble`.

La opción final es usar el visualizador de datos de RStudio para obtener una versión interactiva del data frame completo. Esto también es útil luego de realizar una larga cadena de manipulaciones.


```r
vuelos %>% 
  View()
```

### Selección de subconjuntos

Hasta ahora, todas las herramientas que aprendiste funcionan con el data frame completo. Si quieres recuperar una variable individual, necesitas algunas herramientas nuevas: `$` y `[[`. Mientras que `[[` permite extraer variables usando tanto su nombre como su suposición, con `$` sólo se puede extraer mediante el nombre. La única diferencia es que `$` permite escribir un poco menos.


```r
df <- tibble(
  x = runif(5),
  y = rnorm(5)
)

# Extraer usando el nombre
df$x
#> [1] 0.434 0.395 0.548 0.762 0.254
df[["x"]]
#> [1] 0.434 0.395 0.548 0.762 0.254

# Extraer indicando la posición 
df[[1]]
#> [1] 0.434 0.395 0.548 0.762 0.254
```

Para usarlos con un pipe, necesitarás usar el marcador de posición `.`:


```r
df %>% .$x
#> [1] 0.434 0.395 0.548 0.762 0.254
df %>% .[["x"]]
#> [1] 0.434 0.395 0.548 0.762 0.254
```

En comparación a un `data.frame`, los tibbles son más estrictos: nunca funcionan con  coincidencias parciales, y generan una advertencia si la columna a la que intentas de acceder no existe.

## Interactuando con código previo

Algunas funciones previas no funcionan con tibbles. Si te encuentras uno de esos casos, usa `as.data.frame()` para convertir un tibble de nuevo en un `data.frame`:


```r
class(as.data.frame(tb))
#> [1] "data.frame"
```

La principal razón de que algunas funciones previas no funcionen con tibbles es la función `[`. En este libro no usamos mucho `[` porque `dplyr::filter()` y `dplyr::select()` resuelven los mismos problemas con un código más claro (aprenderás un poco sobre ello en [vector subsetting](#vector-subsetting) XXX). Con los data frames de R base, `[`  a veces devuelve un data frame y a veces devuelve un vector. Con tibbles, `[` siempre devuelve otro tibble.

## Ejercicios


1. ¿Cómo puedes saber si un objeto es un tibble? (Sugerencia: imprime `mtautos` en consola, que es un data frame clásico).

1. Compara y contrasta las siguientes operaciones aplicadas a un `data.frame` y a un tibble equivalente. ¿Qué es diferente? ¿Por qué podría causarte problemas el comportamiento por defecto del data frame?
    
    
    ```r
    df <- data.frame(abc = 1, xyz = "a")
    df$x
    df[, "xyz"]
    df[, c("abc", "xyz")]
    ```

1. Si tienes el nombre de una variable guardada en un objeto, p.e., `var <- "mpg"`, ¿cómo puedes extraer esta variable de un tibble?

1.  Practica referenciar nombres no sintácticos en el siguiente data frame:

    1. Extrayendo la variable llamada `1`.
    
    1. Generando un gráfico de dispersión de `1` vs `2`.
    
    1. Creando una nueva columna llamada `3` que sea el resultado de la división de `2` por `1`.

    1. Renombrando las columnas como `uno`, `dos` y `tres`.
    
    
    ```r
    molesto <- tibble(
      `1` = 1:10,
      `2` = `1` * 2 + rnorm(length(`1`))
    )
    ```

1.  ¿Qué hace `tibble::enframe()`? ¿Cuándo lo usarías?

1. ¿Qué opción controla cuántos nombres de columnas adicionales se muestran al pie de un tibble?
