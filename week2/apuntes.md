Apuntes semana 2
========================================================

Lattice plotting system
------------------------

Multidim data y para hacer muchos de golpe (esto habria venido de la leche en mi tesis)

Esta repartido entre los paquetes lattice y grid (aunque a este se le suele llamar de forma interna) 

Se hace todo con una sola llamada a la funcion, aunque puede ser una llamada larga de narices

Funciones dentro de el

### xyplot 

en general se llama de la forma

xplot( x~y | f * g, data )

f, g conditioning variables * es la interaccion

si no se especifica data se busca en el parent



```r
library(lattice)
library(datasets)

xyplot(Ozone ~ Wind, data = airquality)
```

![plot of chunk unnamed-chunk-1](figure/unnamed-chunk-1.png) 


las condition variables deberian ser factores 


```r
library(lattice)
library(datasets)

airquality <- transform(airquality, Month = factor(Month))

xyplot(Ozone ~ Wind | Month, data = airquality, layout = c(5, 1))
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 





###  bwplot

### histogram

###  stripplot (como un boxplot pero con puntos)

###  splom 

###  levelplot, contourplot 


Comportamiento de Lattice
-------------------------

Lo que devuelven las llamadas es un objeto de clase trellis, que es autoimprimible


```r
library(lattice)
library(datasets)

p <- xyplot(Ozone ~ Wind, data = airquality)
# Aqui no ha pasado nada

print(p)
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

 
 
Lattice panel functions
-----------------------

Sirven para controlar lo que pasa en cada cuadradito
viene con las suyas por defecto pero se pueden tunear

Reciben las coordenadas X/y de cada panel (y ...) 


Primer ejemplo (sin customizar)



```r
set.seed(10)
x <- rnorm(100)
f <- rep(0:1, each = 50)
y <- x + f - f * x + rnorm(100, sd = 0.5)
f <- factor(f, labels = c("Group 1", "Group 2"))
xyplot(y ~ x | f, layout = c(2, 1))  ## Plot with 2 panels
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 


Si customizamos se haria tal que asi


```r
## Custom panel function
xyplot(y ~ x | f, panel = function(x, y, ...) {
    panel.xyplot(x, y, ...)  ## First call the default panel function for 'xyplot'
    panel.abline(h = median(y), lty = 2)  ## Add a horizontal line at the median
})
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 


las opciones se pueden sacar con un panel. y ver que autocompleta


```r
## Custom panel function
xyplot(y ~ x | f, panel = function(x, y, ...) {
    panel.xyplot(x, y, ...)  ## First call default panel function
    panel.lmline(x, y, col = 2)  ## Overlay a simple linear regression line
})
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 


-------------------------------
 
 
ggplot
=============
 
 
