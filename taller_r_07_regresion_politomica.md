Taller 07
================
dacarras
Thu May 25, 2023

------------------------------------------------------------------------

# Instrucciones

- En este taller vamos a volver a emplear los datos del estudio de Poli
  victimizacion de Jovenes, realizada en Chile en Octubre de 2017.

- Los datos que vamos a emplear son una versión recortada de los datos y
  con nombres adaptados, que se espera sean más amigables para generar
  los resultados programando en R.

- El archivo que contiene los datos que vamos a emplear se llama:

<!-- -->


    datos_poli_2017.csv

- El libro de codigos de la base de datos que vamos a emplear, se llama:

<!-- -->


    datos_poli_2017_codebook.xlsx

- **Advertencia**: Los datos originales provienen de una muestra
  probabilística. Este tipo de datos, permite realizar inferencias a la
  población, si la información del diseño es empleada para producir
  estimaciones. En este ejercicio con fines ilustrativos, vamos a
  ignorar este aspecto, y solo vamos a producir resultados descriptivos.

# Referencias

Alvarez, E., Guajardo, H., & Messen, R. (1986). Estudio exploratorio
sobre una escala de autoevaluación para la depresión en niños y
adolescentes. Revista Chilena de Pediatria, 57(1), 21–25.
<https://doi.org/10.4067/s0370-41061986000100003>

Birleson, P., Hudson, I., Buchanan, D. G., & Wolff, S. (1987). Clinical
Evaluation of a Self‐Rating Scale for Depressive Disorder in Childhood
(Depression Self‐Rating Scale). Journal of Child Psychology and
Psychiatry, 28(1), 43–60.
<https://doi.org/10.1111/j.1469-7610.1987.tb00651.x>

Consejo Nacional de la Infancia. (2018). Análisis Multivariable de
Estudio de Polivictimización en Niños, Niñas y Adolescentes realizado
por la Pontificia Universidad Católica de Chile.
<http://biblioteca.digital.gob.cl/handle/123456789/3535>

Denda, K., Kako, Y., Kitagawa, N., & Koyama, T. (2006). Assessment of
depressive symptoms in Japanese school children and adolescents using
the birleson depression self-rating scale. International Journal of
Psychiatry in Medicine, 36(2), 231–241.
<https://doi.org/10.2190/3YCX-H0MT-49DK-C61Q>

MINSAL. (2013). Guía Clínica para el tratamiento de adolescentes de 10 a
14 años con Depresión.
<https://www.guiadisc.com/wp-content/pdfs/guia-clinica-tratamiento-depresion-adolescentes.pdf>

Subsecretaria Prevención del Delito. (2018). Primera Encuesta Nacional
de Polivictimización en Niñas, Niños y Adolescentes: Presentación de
Resultados.

------------------------------------------------------------------------

# Ejercicio 1. Abrir datos y Revisar datos.

- Abra los datos `datos_poli_2017.csv`, empleando la función
  `read.csv()`. Emplee un objeto llamado `data_poli_full` para alojar a
  los datos abiertos.

**Codigo 1.1:** leer datos desde csv.

``` r
# -----------------------------------------------
# abrir datos
# -----------------------------------------------

data_poli_full <- read.csv('datos_poli_2017.csv')
```

**Codigo 1.2:** revisar datos.

- **¿Cuántas variables y cuántos casos posee la base de datos
  original?**
- Indique su respuesta bajo el código.

``` r
# -----------------------------------------------
# revisar datos cargados
# -----------------------------------------------

dplyr::glimpse(data_poli_full)
```

    ## Rows: 19,684
    ## Columns: 46
    ## $ id_i  [3m[38;5;246m<int>[39m[23m 47601, 47602, 47603, 47604, 47605, 47606, 47607, 47608, 47609, 4…
    ## $ curso [3m[38;5;246m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 3, 3, 4…
    ## $ sexo  [3m[38;5;246m<int>[39m[23m 1, 1, 2, 1, 1, 2, 1, 1, 2, 1, 1, 1, 2, 2, 1, 1, 1, 1, 1, 1, 1, 2…
    ## $ edad  [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 2, 2, 2, 3, 3, 2, 3, 2, 3, 3, 3, 3, 4, 3, 3, 4…
    ## $ v01   [3m[38;5;246m<int>[39m[23m 2, 2, 2, 1, 2, 2, 1, 1, 2, 1, 2, 1, 1, 2, 2, 1, 2, 2, 2, 2, 2, 1…
    ## $ v02   [3m[38;5;246m<int>[39m[23m 2, 2, 2, NA, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, NA, 2, 2, 2,…
    ## $ v03   [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 2, 2, 1, 2, 1, 2, 2, 1, 1, 1, 1, 2, 2, 2, 2, 1, 1, 1…
    ## $ v04   [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, NA, 2, 2, 2, …
    ## $ v05   [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ v06   [3m[38;5;246m<int>[39m[23m 2, 2, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 2, 1, 2, 2, 2, 1, 1, 1, 1, 1…
    ## $ v07   [3m[38;5;246m<int>[39m[23m 1, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ au1   [3m[38;5;246m<int>[39m[23m 5, 5, 4, 3, 4, 4, 5, 5, 5, 5, 3, 4, 4, 4, 5, 5, 5, 5, 5, 4, 3, 5…
    ## $ au2   [3m[38;5;246m<int>[39m[23m 5, 5, 5, 2, 4, 4, 5, 5, 5, 5, 3, 4, 4, 4, 5, 4, 5, 5, 5, 4, 4, 5…
    ## $ au3   [3m[38;5;246m<int>[39m[23m 1, 1, 1, 3, 1, 2, 2, 2, 3, 2, 3, 4, 2, 2, 3, 3, 1, 3, 1, 2, 4, 1…
    ## $ au4   [3m[38;5;246m<int>[39m[23m 5, 5, 5, 2, 5, 3, 4, 5, 5, 4, 3, 3, 4, 3, 4, 4, 5, 5, 5, 5, 4, 5…
    ## $ au5   [3m[38;5;246m<int>[39m[23m 1, 2, 1, 2, 2, 4, 1, 1, 1, 1, 3, 3, 2, 1, 5, 4, 1, 1, 1, 2, 5, 1…
    ## $ au6   [3m[38;5;246m<int>[39m[23m 5, 4, 5, 2, 5, 4, 5, 5, 5, 5, 3, 3, 4, 3, 3, 3, 4, 5, 4, 4, 2, 5…
    ## $ au7   [3m[38;5;246m<int>[39m[23m 5, 4, 5, 1, 4, 3, 5, 5, 5, 5, 3, 4, 3, 5, 2, 4, 5, 5, 5, 3, 2, 5…
    ## $ au8   [3m[38;5;246m<int>[39m[23m 1, 2, 2, 5, 4, 3, 5, 2, 1, 4, 3, 5, 3, 2, 5, 4, 1, 1, 2, 3, 2, 1…
    ## $ au9   [3m[38;5;246m<int>[39m[23m 1, 2, 1, 4, 2, 2, 2, 2, 1, 4, 3, 5, 2, 4, 4, 3, 3, 3, 2, 2, 4, 1…
    ## $ au10  [3m[38;5;246m<int>[39m[23m 1, 1, 1, 4, 1, 3, 2, 3, 1, 4, 4, 2, 2, 2, 5, 4, 2, 2, 2, 1, 2, 1…
    ## $ d01   [3m[38;5;246m<int>[39m[23m 3, 2, 2, 2, 2, 3, 3, 1, 3, 2, 2, 2, 3, 2, 3, 2, 2, 3, 3, 2, 1, 2…
    ## $ d02   [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 3, 2, 3, 3, 1, 2, 2, 1, 2, 2, 2, 3, 2, 1…
    ## $ d03   [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 3, 3, 1, 1, 3, 1, 1, 1, 1, 2, 1, 1…
    ## $ d04   [3m[38;5;246m<int>[39m[23m 1, 2, 2, 1, 1, 1, 1, 1, 2, 1, 2, 2, 2, 1, 2, 2, 2, 1, 1, 2, 2, 1…
    ## $ d05   [3m[38;5;246m<int>[39m[23m 2, 2, 2, 1, 3, 2, 3, 3, 2, 1, 2, 2, 2, 1, 1, 1, 1, 2, 2, 1, 1, 2…
    ## $ d06   [3m[38;5;246m<int>[39m[23m 3, 1, 3, 2, 2, 2, 3, 3, 1, 2, 2, 1, 1, 3, 2, 2, 3, 3, 2, 2, 2, 3…
    ## $ d07   [3m[38;5;246m<int>[39m[23m 2, 2, 3, 1, 2, 2, 2, 3, 3, 3, 2, 2, 3, 2, 3, 2, 2, 3, 2, 2, 1, 3…
    ## $ d08   [3m[38;5;246m<int>[39m[23m 3, 3, 3, 3, 3, 3, 3, 3, 2, 3, 3, 2, 2, 3, 3, 3, 3, 3, 3, 3, 2, 3…
    ## $ d09   [3m[38;5;246m<int>[39m[23m 2, 3, 3, 1, 2, 3, 1, 3, 3, 2, 2, 3, 2, 3, 2, 3, 3, 2, 3, 2, 2, 3…
    ## $ d10   [3m[38;5;246m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 1, 1, 1, 1, 2, 1…
    ## $ d11   [3m[38;5;246m<int>[39m[23m 3, 2, 3, 2, 2, 2, 2, 3, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 2, 3…
    ## $ d12   [3m[38;5;246m<int>[39m[23m 3, 3, 3, 2, 2, 2, 2, 3, 1, 3, 2, 2, 2, 3, 2, 3, 3, 3, 3, 2, 1, 3…
    ## $ d13   [3m[38;5;246m<int>[39m[23m 2, 3, 3, 2, 3, 2, 3, 3, 1, 3, 1, 2, 2, 3, 3, 3, 3, 3, 3, 2, 1, 3…
    ## $ d14   [3m[38;5;246m<int>[39m[23m 1, 1, 2, 1, 2, 1, 1, 1, 2, 2, 2, 3, 1, 1, 1, 2, 1, 1, 1, 1, 1, 1…
    ## $ d15   [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 2, 3, 1, 1, 2, 2, 1, 2, 1, 3, NA, …
    ## $ d16   [3m[38;5;246m<int>[39m[23m 2, 3, 3, 2, 2, 3, 3, 3, 3, 3, 2, 2, 2, 2, 3, 2, 2, 3, 3, 2, 1, 3…
    ## $ d17   [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 3, 1, 1, 2, 1, 1, 1, 1, 3, 2, 1…
    ## $ d18   [3m[38;5;246m<int>[39m[23m 2, 2, 2, 3, 2, 2, 1, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 1, 2, 3, 3, 1…
    ## $ self  [3m[38;5;246m<int>[39m[23m 50, 45, 48, 22, 42, 34, 42, 45, 48, 39, 29, 29, 38, 38, 27, 32, …
    ## $ dep   [3m[38;5;246m<int>[39m[23m 7, 9, 6, 18, 10, 7, 6, 4, 17, 12, 19, 22, 10, 8, 14, 11, 8, 4, 5…
    ## $ adm   [3m[38;5;246m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ zona  [3m[38;5;246m<int>[39m[23m 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4…
    ## $ prio  [3m[38;5;246m<dbl>[39m[23m 0.1644245, 0.1644245, 0.1644245, 0.1644245, 0.1644245, 0.1644245…
    ## $ comu  [3m[38;5;246m<int>[39m[23m 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115,…
    ## $ poli  [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…

- Respuesta
  - Casos: \[escribir aqui la cantidad de casos, y borrar los
    corchetes\]
  - Variables: \[escribir aqui la cantidad de variables, y borrar los
    corchetes\]

# Ejercicio 2. Recodificación de variable de muchos valores.

Recodifique la variable `edad` en una nueva variable `edad_cat` que
contenga tres grupos:

- Grupo A: estudiantes de 12 a 13 años
- Grupo B: estudiantes de 14 a 15 años
- Grupo C: estudiantes de 16 años o más

**Codigo 2.1:** recodificar variable continua en tramos.

``` r
# -----------------------------------------------
# información de la variable a recodificar
# -----------------------------------------------

# variable: edad
# Edad en tramos
# [1] 12 años
# [2] 13 años
# [3] 14 años
# [4] 15 años
# [5] 16 años
# [6] 17 años o más

# -----------------------------------------------
# recodicacion de variable continua en tramos.
# -----------------------------------------------

library(dplyr)
data_poli   <- data_poli_full %>%
               mutate(edad_cat = case_when(
               between(edad, 1,  2) ~ 'Grupo A',
               between(edad, 3,  4) ~ 'Grupo B',
               between(edad, 5,  6) ~ 'Grupo C'
               )) %>%
               # eliminar datos sin edad
               dplyr::filter(between(edad, 1,6)) %>%
               dplyr::glimpse()
```

    ## Rows: 19,433
    ## Columns: 47
    ## $ id_i     [3m[38;5;246m<int>[39m[23m 47601, 47602, 47603, 47604, 47605, 47606, 47607, 47608, 47609…
    ## $ curso    [3m[38;5;246m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 3, 3…
    ## $ sexo     [3m[38;5;246m<int>[39m[23m 1, 1, 2, 1, 1, 2, 1, 1, 2, 1, 1, 1, 2, 2, 1, 1, 1, 1, 1, 1, 1…
    ## $ edad     [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 2, 2, 2, 3, 3, 2, 3, 2, 3, 3, 3, 3, 4, 3, 3…
    ## $ v01      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 1, 2, 2, 1, 1, 2, 1, 2, 1, 1, 2, 2, 1, 2, 2, 2, 2, 2…
    ## $ v02      [3m[38;5;246m<int>[39m[23m 2, 2, 2, NA, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, NA, 2, 2,…
    ## $ v03      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 2, 2, 1, 2, 1, 2, 2, 1, 1, 1, 1, 2, 2, 2, 2, 1, 1…
    ## $ v04      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, NA, 2, 2, …
    ## $ v05      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ v06      [3m[38;5;246m<int>[39m[23m 2, 2, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 2, 1, 2, 2, 2, 1, 1, 1, 1…
    ## $ v07      [3m[38;5;246m<int>[39m[23m 1, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ au1      [3m[38;5;246m<int>[39m[23m 5, 5, 4, 3, 4, 4, 5, 5, 5, 5, 3, 4, 4, 4, 5, 5, 5, 5, 5, 4, 3…
    ## $ au2      [3m[38;5;246m<int>[39m[23m 5, 5, 5, 2, 4, 4, 5, 5, 5, 5, 3, 4, 4, 4, 5, 4, 5, 5, 5, 4, 4…
    ## $ au3      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 3, 1, 2, 2, 2, 3, 2, 3, 4, 2, 2, 3, 3, 1, 3, 1, 2, 4…
    ## $ au4      [3m[38;5;246m<int>[39m[23m 5, 5, 5, 2, 5, 3, 4, 5, 5, 4, 3, 3, 4, 3, 4, 4, 5, 5, 5, 5, 4…
    ## $ au5      [3m[38;5;246m<int>[39m[23m 1, 2, 1, 2, 2, 4, 1, 1, 1, 1, 3, 3, 2, 1, 5, 4, 1, 1, 1, 2, 5…
    ## $ au6      [3m[38;5;246m<int>[39m[23m 5, 4, 5, 2, 5, 4, 5, 5, 5, 5, 3, 3, 4, 3, 3, 3, 4, 5, 4, 4, 2…
    ## $ au7      [3m[38;5;246m<int>[39m[23m 5, 4, 5, 1, 4, 3, 5, 5, 5, 5, 3, 4, 3, 5, 2, 4, 5, 5, 5, 3, 2…
    ## $ au8      [3m[38;5;246m<int>[39m[23m 1, 2, 2, 5, 4, 3, 5, 2, 1, 4, 3, 5, 3, 2, 5, 4, 1, 1, 2, 3, 2…
    ## $ au9      [3m[38;5;246m<int>[39m[23m 1, 2, 1, 4, 2, 2, 2, 2, 1, 4, 3, 5, 2, 4, 4, 3, 3, 3, 2, 2, 4…
    ## $ au10     [3m[38;5;246m<int>[39m[23m 1, 1, 1, 4, 1, 3, 2, 3, 1, 4, 4, 2, 2, 2, 5, 4, 2, 2, 2, 1, 2…
    ## $ d01      [3m[38;5;246m<int>[39m[23m 3, 2, 2, 2, 2, 3, 3, 1, 3, 2, 2, 2, 3, 2, 3, 2, 2, 3, 3, 2, 1…
    ## $ d02      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 3, 2, 3, 3, 1, 2, 2, 1, 2, 2, 2, 3, 2…
    ## $ d03      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 3, 3, 1, 1, 3, 1, 1, 1, 1, 2, 1…
    ## $ d04      [3m[38;5;246m<int>[39m[23m 1, 2, 2, 1, 1, 1, 1, 1, 2, 1, 2, 2, 2, 1, 2, 2, 2, 1, 1, 2, 2…
    ## $ d05      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 1, 3, 2, 3, 3, 2, 1, 2, 2, 2, 1, 1, 1, 1, 2, 2, 1, 1…
    ## $ d06      [3m[38;5;246m<int>[39m[23m 3, 1, 3, 2, 2, 2, 3, 3, 1, 2, 2, 1, 1, 3, 2, 2, 3, 3, 2, 2, 2…
    ## $ d07      [3m[38;5;246m<int>[39m[23m 2, 2, 3, 1, 2, 2, 2, 3, 3, 3, 2, 2, 3, 2, 3, 2, 2, 3, 2, 2, 1…
    ## $ d08      [3m[38;5;246m<int>[39m[23m 3, 3, 3, 3, 3, 3, 3, 3, 2, 3, 3, 2, 2, 3, 3, 3, 3, 3, 3, 3, 2…
    ## $ d09      [3m[38;5;246m<int>[39m[23m 2, 3, 3, 1, 2, 3, 1, 3, 3, 2, 2, 3, 2, 3, 2, 3, 3, 2, 3, 2, 2…
    ## $ d10      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 1, 1, 1, 1, 2…
    ## $ d11      [3m[38;5;246m<int>[39m[23m 3, 2, 3, 2, 2, 2, 2, 3, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 2…
    ## $ d12      [3m[38;5;246m<int>[39m[23m 3, 3, 3, 2, 2, 2, 2, 3, 1, 3, 2, 2, 2, 3, 2, 3, 3, 3, 3, 2, 1…
    ## $ d13      [3m[38;5;246m<int>[39m[23m 2, 3, 3, 2, 3, 2, 3, 3, 1, 3, 1, 2, 2, 3, 3, 3, 3, 3, 3, 2, 1…
    ## $ d14      [3m[38;5;246m<int>[39m[23m 1, 1, 2, 1, 2, 1, 1, 1, 2, 2, 2, 3, 1, 1, 1, 2, 1, 1, 1, 1, 1…
    ## $ d15      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 2, 3, 1, 1, 2, 2, 1, 2, 1, 3, N…
    ## $ d16      [3m[38;5;246m<int>[39m[23m 2, 3, 3, 2, 2, 3, 3, 3, 3, 3, 2, 2, 2, 2, 3, 2, 2, 3, 3, 2, 1…
    ## $ d17      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 3, 1, 1, 2, 1, 1, 1, 1, 3, 2…
    ## $ d18      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 3, 2, 2, 1, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 1, 2, 3, 3…
    ## $ self     [3m[38;5;246m<int>[39m[23m 50, 45, 48, 22, 42, 34, 42, 45, 48, 39, 29, 29, 38, 38, 27, 3…
    ## $ dep      [3m[38;5;246m<int>[39m[23m 7, 9, 6, 18, 10, 7, 6, 4, 17, 12, 19, 22, 10, 8, 14, 11, 8, 4…
    ## $ adm      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ zona     [3m[38;5;246m<int>[39m[23m 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4…
    ## $ prio     [3m[38;5;246m<dbl>[39m[23m 0.1644245, 0.1644245, 0.1644245, 0.1644245, 0.1644245, 0.1644…
    ## $ comu     [3m[38;5;246m<int>[39m[23m 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 115, 1…
    ## $ poli     [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ edad_cat [3m[38;5;246m<chr>[39m[23m "Grupo A", "Grupo A", "Grupo A", "Grupo A", "Grupo A", "Grupo…

``` r
# Nota: edad es discreta (no tiene decimales)

# -----------------------------------------------
# revision de la variable generada
# -----------------------------------------------

data_poli %>%
group_by(edad_cat) %>%
summarize(
edad_min = min(edad, na.rm = TRUE),
edad_max = max(edad, na.rm = TRUE),
n = n()
) %>%
knitr::kable(., digits = 2)
```

| edad_cat | edad_min | edad_max |    n |
|:---------|---------:|---------:|-----:|
| Grupo A  |        1 |        2 | 5534 |
| Grupo B  |        3 |        4 | 7474 |
| Grupo C  |        5 |        6 | 6425 |

> Nota: no es recomendable borrar datos, cuando estos estan perdidos en
> cualquier escenarios. En este caso, estamos borrando datos sin datos
> observados en la variable de edad solo con propositos ilustrativos.

# Ejercicio 3. Crear una muestra de los datos originales.

Vamos a crear una muestra de 500 casos, y vamos a emplear un seed
generico con `set.seed(123456)`; y además vamos a revisar las
proporciones de casos son las que nos quedamos.

``` r
# -----------------------------------------------
# muestra de 500 casos
# -----------------------------------------------

set.seed(123456)
library(dplyr)
data_model <- dplyr::slice_sample(data_poli, n = 500)


# -----------------------------------------------
# revision de la variable generada
# -----------------------------------------------

data_model %>%
group_by(edad_cat) %>%
summarize(
n = n()
) %>%
mutate(p = n/sum(n)) %>%
knitr::kable(., digits = 2)
```

| edad_cat |   n |    p |
|:---------|----:|-----:|
| Grupo A  | 144 | 0.29 |
| Grupo B  | 194 | 0.39 |
| Grupo C  | 162 | 0.32 |

# Ejercicio 4. Medias descriptivas de la variable de respuesta.

Vamos a emplear a la variable `dep`, como la variable de respuesta. Esta
variable posee los puntajes de escala de Birleson de depresión. En este
ejercicio, antes de ajustar modelos de regresión, vamos a calcular las
medias descriptivas de cada uno de los grupos etarios que creamos, los
grupos a, b, y c; alojados en la variable `edad_cat`.

``` r
# -----------------------------------------------
# medias de depresion por grupo
# -----------------------------------------------

data_model %>%
group_by(edad_cat) %>%
summarize(
media_depresion = mean(dep, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| edad_cat | media_depresion |
|:---------|----------------:|
| Grupo A  |           11.31 |
| Grupo B  |           12.01 |
| Grupo C  |           12.58 |

**¿Qué medias posee cada grupo?**

- **Respuesta**
  - Media grupo A: `11.31`
  - Media grupo B: `12.01`
  - Media grupo C: `12.58`

# Ejercicio 5. Crear variables indicadoras

A partir de la variable `edad_cat` vamos a crear variables indicadoras.
Vamos a generar estas variables para cada uno de los tramos de edad que
creamos anteriormente.

``` r
# -----------------------------------------------
# creación de variables indicadoras (dummies)
# -----------------------------------------------

data_model <- data_model %>%
              mutate(grupo_a = dplyr::if_else(edad_cat == 'Grupo A', 1, 0)) %>%
              mutate(grupo_b = dplyr::if_else(edad_cat == 'Grupo B', 1, 0)) %>%
              mutate(grupo_c = dplyr::if_else(edad_cat == 'Grupo C', 1, 0)) %>%
              dplyr::glimpse()
```

    ## Rows: 500
    ## Columns: 50
    ## $ id_i     [3m[38;5;246m<int>[39m[23m 50621, 22614, 45404, 77625, 25809, 74419, 21832, 10703, 83511…
    ## $ curso    [3m[38;5;246m<int>[39m[23m 4, 3, 3, 5, 2, 1, 3, 1, 3, 3, 3, 5, 1, 1, 2, 5, 2, 4, 5, 3, 2…
    ## $ sexo     [3m[38;5;246m<int>[39m[23m 2, 1, 1, 2, 1, 2, 2, 1, 2, 1, 1, 2, 2, 1, 1, 2, 2, 2, 1, 1, 2…
    ## $ edad     [3m[38;5;246m<int>[39m[23m 5, 4, 4, 6, 3, 2, 4, 3, 4, 3, 5, 6, 4, 1, 2, 5, 3, 5, 6, 4, 2…
    ## $ v01      [3m[38;5;246m<int>[39m[23m 1, 2, 2, 1, 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2…
    ## $ v02      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2…
    ## $ v03      [3m[38;5;246m<int>[39m[23m 1, 2, 2, 1, 2, 1, 1, 2, 1, 2, 2, 2, 2, 2, 1, 1, 2, 2, 2, NA, …
    ## $ v04      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 1, 2, 1, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ v05      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ v06      [3m[38;5;246m<int>[39m[23m 1, 2, 2, 1, 2, 2, 1, 1, 1, 2, 2, 1, 1, 2, 1, 2, 2, 2, 1, 1, 2…
    ## $ v07      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 2, 2, 2, 2…
    ## $ au1      [3m[38;5;246m<int>[39m[23m 4, 5, 4, 4, 4, 4, 3, 4, 4, 4, 3, 5, 3, 4, 3, 3, 4, 3, 5, 5, 4…
    ## $ au2      [3m[38;5;246m<int>[39m[23m 4, 5, 4, 4, 4, 4, 4, 4, 4, 4, 4, 5, 4, 4, 4, 4, 4, 3, 5, 5, 4…
    ## $ au3      [3m[38;5;246m<int>[39m[23m 2, 3, 2, 3, 2, 3, 2, 4, 1, 2, 3, 1, 3, 3, 4, 3, 1, 3, 1, 2, 1…
    ## $ au4      [3m[38;5;246m<int>[39m[23m 4, 2, 3, 4, 5, 5, 4, 4, 5, 4, 3, 5, 4, 4, 4, 4, 5, 3, 5, 5, 4…
    ## $ au5      [3m[38;5;246m<int>[39m[23m 3, 3, 2, 3, 2, 3, 2, 4, 1, 2, 3, 4, NA, 3, 2, 4, 5, 2, 1, 1, …
    ## $ au6      [3m[38;5;246m<int>[39m[23m 4, 3, 4, 3, 5, 5, 2, 2, 5, 2, 3, 5, 4, 4, 3, 4, 5, 5, 4, 5, 4…
    ## $ au7      [3m[38;5;246m<int>[39m[23m 4, 4, 3, 4, 5, 4, 3, 2, 5, 3, 3, 4, 4, 4, 4, 3, 5, 4, 4, 5, 4…
    ## $ au8      [3m[38;5;246m<int>[39m[23m 3, 3, 4, 5, NA, 5, 3, 4, 5, 5, 3, 2, 4, 4, 4, 3, 2, 4, 5, 5, …
    ## $ au9      [3m[38;5;246m<int>[39m[23m 2, 3, 3, 4, 2, 5, 4, 4, 1, 4, 2, 2, 3, 3, 3, NA, 1, 4, 1, 1, …
    ## $ au10     [3m[38;5;246m<int>[39m[23m 2, 4, 3, 4, 2, 4, 3, 4, 1, 3, 2, 1, 3, 4, 3, 2, 2, 4, 1, 3, 1…
    ## $ d01      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 3, 2, 1, 2, 2, 3, 3, 2, 2, 2, 2, 2, 2, 1, 2, 3, 3, 1…
    ## $ d02      [3m[38;5;246m<int>[39m[23m 1, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 3, 2, 2, 1, 2, 2, 1…
    ## $ d03      [3m[38;5;246m<int>[39m[23m 2, 1, 2, 1, 1, 1, 1, 2, 1, 2, 2, 3, 2, 1, 2, 1, 2, 1, 2, 2, 1…
    ## $ d04      [3m[38;5;246m<int>[39m[23m 2, 1, 1, 1, 2, 2, 1, 2, 1, 2, 2, 1, 2, 1, 1, 2, 1, 1, 2, 2, 1…
    ## $ d05      [3m[38;5;246m<int>[39m[23m 3, 2, 1, 1, 2, 3, 2, 1, 3, 2, 2, 2, 2, 2, 2, 1, 1, 2, 1, 2, N…
    ## $ d06      [3m[38;5;246m<int>[39m[23m 1, 3, 3, 2, 3, 3, 3, 1, 3, 3, 2, 3, 3, 3, 2, 2, 3, 2, 3, 3, N…
    ## $ d07      [3m[38;5;246m<int>[39m[23m 2, 3, 2, 2, 3, 3, 2, 1, 3, 2, 3, 2, 2, 3, 2, 2, 3, 2, 3, 2, N…
    ## $ d08      [3m[38;5;246m<int>[39m[23m 3, 3, 3, 3, 3, 3, 3, 2, 3, 2, 3, 3, 2, 3, 2, 3, 3, 2, 3, 3, N…
    ## $ d09      [3m[38;5;246m<int>[39m[23m 2, 3, 3, 2, 3, 3, 3, 2, 3, 2, 3, 3, 2, 3, 2, 2, 2, 2, 3, 3, 3…
    ## $ d10      [3m[38;5;246m<int>[39m[23m 1, 1, 1, 1, 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 1, 1, 1…
    ## $ d11      [3m[38;5;246m<int>[39m[23m 2, 2, 2, 2, 3, 3, 2, 2, 3, 2, 2, 2, 2, NA, 2, 2, 2, 2, 3, 2, …
    ## $ d12      [3m[38;5;246m<int>[39m[23m 2, 3, 2, 2, 3, 3, 2, 2, 3, 2, 2, 2, 2, 2, 2, 3, 3, 2, 3, 3, 3…
    ## $ d13      [3m[38;5;246m<int>[39m[23m 2, 3, 3, 2, 3, 3, 3, 2, 3, 3, 2, 2, 3, 1, 3, 2, 3, 2, 3, 3, 3…
    ## $ d14      [3m[38;5;246m<int>[39m[23m 2, 1, 1, 1, 2, 2, 2, 3, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 1, 1, 1…
    ## $ d15      [3m[38;5;246m<int>[39m[23m 3, 1, 1, 2, 1, 2, 2, 3, 1, 2, 2, 1, 1, 1, 2, 1, 2, 2, 2, 1, 1…
    ## $ d16      [3m[38;5;246m<int>[39m[23m 3, 2, 2, 2, 3, 2, 1, 2, 3, 3, 2, 2, 2, 3, 2, 3, 2, 3, 2, 3, 3…
    ## $ d17      [3m[38;5;246m<int>[39m[23m 1, 1, 2, 2, 1, 2, 1, 3, 1, 2, 1, 1, 1, 1, 2, 1, 2, 1, 1, 2, 1…
    ## $ d18      [3m[38;5;246m<int>[39m[23m 2, 1, 1, 2, 1, 2, 2, 3, 1, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 1…
    ## $ self     [3m[38;5;246m<int>[39m[23m 38, 33, 34, 30, NA, 32, 32, 26, 44, 31, 33, 44, NA, 33, 32, N…
    ## $ dep      [3m[38;5;246m<int>[39m[23m 14, 5, 10, 12, 5, 10, 10, 25, 1, 12, 12, 11, 12, NA, 16, 12, …
    ## $ adm      [3m[38;5;246m<int>[39m[23m 1, 2, 1, 2, 2, 2, 2, 2, 1, 2, 1, 1, 1, 1, 1, 2, 2, 2, 2, 1, 2…
    ## $ zona     [3m[38;5;246m<int>[39m[23m 3, 2, 3, 2, 3, 3, 2, 1, 4, 1, 3, 3, 2, 3, 3, 2, 4, 1, 1, 4, 4…
    ## $ prio     [3m[38;5;246m<dbl>[39m[23m 0.8587258, 0.4168157, 0.8679654, 0.1720930, 0.3947858, 0.6242…
    ## $ comu     [3m[38;5;246m<int>[39m[23m 93, 50, 37, 188, 45, 137, 170, 68, 149, 44, 39, 116, 152, 85,…
    ## $ poli     [3m[38;5;246m<int>[39m[23m 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
    ## $ edad_cat [3m[38;5;246m<chr>[39m[23m "Grupo C", "Grupo B", "Grupo B", "Grupo C", "Grupo B", "Grupo…
    ## $ grupo_a  [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1…
    ## $ grupo_b  [3m[38;5;246m<dbl>[39m[23m 0, 1, 1, 0, 1, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0…
    ## $ grupo_c  [3m[38;5;246m<dbl>[39m[23m 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 1, 0, 0…

``` r
# -----------------------------------------------
# revision de dummies generadas
# -----------------------------------------------

dplyr::count(data_model, edad_cat, grupo_a)
```

    ##   edad_cat grupo_a   n
    ## 1  Grupo A       1 144
    ## 2  Grupo B       0 194
    ## 3  Grupo C       0 162

``` r
dplyr::count(data_model, edad_cat, grupo_b)
```

    ##   edad_cat grupo_b   n
    ## 1  Grupo A       0 144
    ## 2  Grupo B       1 194
    ## 3  Grupo C       0 162

``` r
dplyr::count(data_model, edad_cat, grupo_c)
```

    ##   edad_cat grupo_c   n
    ## 1  Grupo A       0 144
    ## 2  Grupo B       0 194
    ## 3  Grupo C       1 162

``` r
# -----------------------------------------------
# observacion de diagonal
# -----------------------------------------------

data_model %>%
arrange(edad) %>%
dplyr::select(grupo_a, grupo_b, grupo_c) %>%
unique() %>%
knitr::kable(., digits = 2)
```

|     | grupo_a | grupo_b | grupo_c |
|:----|--------:|--------:|--------:|
| 1   |       1 |       0 |       0 |
| 145 |       0 |       1 |       0 |
| 339 |       0 |       0 |       1 |

# Ejercicio 6. Realize una regresión múltiple prediciendo por grupos de edad.

Realize un modelo de regresión múltiple para determinar si los grupos de
edad (`edad_cat`) predicen de forma estadisticamente significativa la
variable de respuesta `matrimonio`. Muestre los resultados del modelo
usando el comando `summary()`

``` r
# -----------------------------------------------
# grupo_a es referencia (i.e., es intercepto)
# -----------------------------------------------

lm(dep ~ 1 + grupo_b + grupo_c, data = data_model) %>%
summary()
```

    ## 
    ## Call:
    ## lm(formula = dep ~ 1 + grupo_b + grupo_c, data = data_model)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -12.0114  -4.5789  -0.5789   3.6923  21.6923 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  11.3077     0.5488  20.604   <2e-16 ***
    ## grupo_b       0.7037     0.7236   0.972   0.3314    
    ## grupo_c       1.2713     0.7475   1.701   0.0897 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 6.257 on 455 degrees of freedom
    ##   (42 observations deleted due to missingness)
    ## Multiple R-squared:  0.006318,   Adjusted R-squared:  0.001951 
    ## F-statistic: 1.447 on 2 and 455 DF,  p-value: 0.2365

``` r
# -----------------------------------------------
# grupo_b es referencia (i.e., es intercepto)
# -----------------------------------------------

lm(dep ~ 1 + grupo_a + grupo_c, data = data_model) %>%
summary()
```

    ## 
    ## Call:
    ## lm(formula = dep ~ 1 + grupo_a + grupo_c, data = data_model)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -12.0114  -4.5789  -0.5789   3.6923  21.6923 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  12.0114     0.4717  25.466   <2e-16 ***
    ## grupo_a      -0.7037     0.7236  -0.972    0.331    
    ## grupo_c       0.5676     0.6929   0.819    0.413    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 6.257 on 455 degrees of freedom
    ##   (42 observations deleted due to missingness)
    ## Multiple R-squared:  0.006318,   Adjusted R-squared:  0.001951 
    ## F-statistic: 1.447 on 2 and 455 DF,  p-value: 0.2365

``` r
# -----------------------------------------------
# grupo_c es referencia (i.e., es intercepto)
# -----------------------------------------------

lm(dep ~ 1 + grupo_a + grupo_b, data = data_model) %>%
summary()
```

    ## 
    ## Call:
    ## lm(formula = dep ~ 1 + grupo_a + grupo_b, data = data_model)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -12.0114  -4.5789  -0.5789   3.6923  21.6923 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  12.5789     0.5075  24.785   <2e-16 ***
    ## grupo_a      -1.2713     0.7475  -1.701   0.0897 .  
    ## grupo_b      -0.5676     0.6929  -0.819   0.4131    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 6.257 on 455 degrees of freedom
    ##   (42 observations deleted due to missingness)
    ## Multiple R-squared:  0.006318,   Adjusted R-squared:  0.001951 
    ## F-statistic: 1.447 on 2 and 455 DF,  p-value: 0.2365

# Ejercicio 7. Reporte los resultados del modelo de regresión múltiple

Calcule o identifique los siguientes elementos, empleando el primer
modelo, donde el grupo_a es la referencia.

- Media del grupo A
- Media del grupo B
- Media del grupo C
- Desviación estándar de los residuos
- Numero de casos
- Estadígrafo F

``` r
# -----------------------------------------------
# modelo 1
# -----------------------------------------------

# > lm(dep ~ 1 + grupo_b + grupo_c, data = data_model) %>%
# + summary()
# 
# Call:
# lm(formula = dep ~ 1 + grupo_b + grupo_c, data = data_model)
# 
# Residuals:
#      Min       1Q   Median       3Q      Max 
# -12.0114  -4.5789  -0.5789   3.6923  21.6923 
# 
# Coefficients:
#             Estimate Std. Error t value Pr(>|t|)    
# (Intercept)  11.3077     0.5488  20.604   <2e-16 ***
# grupo_b       0.7037     0.7236   0.972   0.3314    
# grupo_c       1.2713     0.7475   1.701   0.0897 .  
# ---
# Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
# 
# Residual standard error: 6.257 on 455 degrees of freedom
#   (42 observations deleted due to missingness)
# Multiple R-squared:  0.006318,  Adjusted R-squared:  0.001951 
# F-statistic: 1.447 on 2 and 455 DF,  p-value: 0.2365

# -----------------------------------------------
# terminos solicitados
# -----------------------------------------------

b1 <- 11.3077 # intercepto (dummie grupo_a)
b2 <- 0.7037  # pendiente dummie grupo_b
b3 <- 1.2713  # pendiente dummie grupo_c

sigma <- 6.257

df1 <- 2
df2 <- 455


media_a <- b1
media_b <- b1 + b2
media_c <- b1 + b3
dev_res <- sigma
num_obs <- df1 + df2 + 1
f_stat  <- 1.447


# -----------------------------------------------
# evidencias de que los resultados son correctos
# -----------------------------------------------

data_model %>%
dplyr::select(dep, grupo_b, grupo_c) %>%
na.omit() %>%
nrow()
```

    ## [1] 458

``` r
# -----------------------------------------------
# tabla de resultados solicitados
# -----------------------------------------------

data.frame(
stat  = c('media_a','media_b', 'media_c', 'dev_res','num_obs','f_stat'),
value = c(media_a,media_b, media_c, dev_res, num_obs, f_stat)
) %>%
knitr::kable(., digits = 2)
```

| stat    |  value |
|:--------|-------:|
| media_a |  11.31 |
| media_b |  12.01 |
| media_c |  12.58 |
| dev_res |   6.26 |
| num_obs | 458.00 |
| f_stat  |   1.45 |

- **Respuesta**

  - Media del grupo A: 11.3077
  - Media del grupo B: 12.0114
  - Media del grupo C: 12.579
  - Desviación estándar de los residuos: 6.257
  - Numero de casos: 458
  - Estadígrafo F: 1.447

# Ejercicio 8. Hipótesis estadisticas

Hagamos un ejercicio de fomrulacion de hipotesis y de descripción de
resultados. Vamos a formular la hipotesis nula que estaría evaluando la
regresion simple, en que incluimos a las variables indicadoras de los
grupos b y c.

Vamos a: - Formular la hipotesis nula - Formular la hipotesis
alternativa - Vamos a reportar al estadistico respectivo para indicar si
la hipotesis nula es adecuada al caso.

- **Respuesta**
  - **Hipotesis nula:** La hipotesis nula puede ser formulada como: la
    diferencia de medias entre los grupos a, b, y c, es igual a cero en
    cada par de comparación.
  - **Hipotesis alternativa:** La hipotesis alternativa para la
    comparación de medias de los puntajes de depresión, es que es que al
    menos una de las diferencia de medias entre los grupos a, b, y c, es
    diferente de cero.
  - **Decisión (con justificación)**: Considerando los resultados
    encontrados, no tenemos evidencias para indicar que hay diferencias
    entre las medias comparadas (F(2,455) = 1.447, p = .24).

# Ejercicio 9. Diferencias de medias

Considerando la respuesta a la pregunta anterior, cuando corresponda
indique si hay evidencia estadisticamente significativa de una
diferencia entre (i) el grupo A y el grupo B y (ii) entre el grupo A y
grupo C. Indique en que partes del resultado del análisis se basa para
responder.

- **Respuesta**

- No se observan diferencias significativas entre los pares de
  comparacion A vs B, y A vs C.

- El coeficiente, que compara a A vs B es 0.7037, y presenta un t de
  tamaño pequeño (t = 0.972, p = .33)

- El coeficiente, que compara a A vs C es 1.2713, y presenta un t de
  tamaño pequeño (t = 1.701, p = .09)

# Ejercicio 10. Más diferencias de medias

Si quisiera obtener directamente en el resultado de la regresión las
comparaciones (i) entre el grupo A y C y (ii) entre el grupo B y C, ¿Que
tendríamos que cambiar en los predictores del modelo de regresión?

``` r
lm(dep ~ 1 + grupo_a + grupo_b, data = data_model) %>%
summary()
```

    ## 
    ## Call:
    ## lm(formula = dep ~ 1 + grupo_a + grupo_b, data = data_model)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -12.0114  -4.5789  -0.5789   3.6923  21.6923 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  12.5789     0.5075  24.785   <2e-16 ***
    ## grupo_a      -1.2713     0.7475  -1.701   0.0897 .  
    ## grupo_b      -0.5676     0.6929  -0.819   0.4131    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 6.257 on 455 degrees of freedom
    ##   (42 observations deleted due to missingness)
    ## Multiple R-squared:  0.006318,   Adjusted R-squared:  0.001951 
    ## F-statistic: 1.447 on 2 and 455 DF,  p-value: 0.2365

``` r
# Nota: se deja como intercepto al grupo c
```

- **Respuesta**

- Como los modelos de regresion de 3 grupos, requieren de un punto de
  referencia, nos basta con dejar la media del grupo c como intercepto.
  Con este cambio, los coeficientes generados por el modelo, son las
  diferencias respectivas de cada grupo respecto a la media del grupo
  c. Un modelo de regresion que permite obtener inferencias sobre las
  diferencias de media de interes es:

<!-- -->


    lm(dep ~ 1 + grupo_a + grupo_b, data = data_model) %>%
    summary()

# Ejercicio 11. ANOVA

Realize un ANOVA evaluando las diferencias de medias entre los grupos A,
B y C respecto de la variable `dep` y genere el análisis de
comparaciones múltiples de Tukey. Reporte si el análisis identifica
diferencias estadisticamente significativas entre los grupos B y C.

``` r
aov(dep ~ edad_cat, data = data_model) %>%
summary()
```

    ##              Df Sum Sq Mean Sq F value Pr(>F)
    ## edad_cat      2    113   56.64   1.447  0.236
    ## Residuals   455  17815   39.15               
    ## 42 observations deleted due to missingness

``` r
anova_model <- aov(dep ~ edad_cat, data = data_model)

TukeyHSD(x=anova_model, 'edad_cat', conf.level=0.95)
```

    ##   Tukey multiple comparisons of means
    ##     95% family-wise confidence level
    ## 
    ## Fit: aov(formula = dep ~ edad_cat, data = data_model)
    ## 
    ## $edad_cat
    ##                      diff        lwr      upr     p adj
    ## Grupo B-Grupo A 0.7036713 -0.9978776 2.405220 0.5946930
    ## Grupo C-Grupo A 1.2712551 -0.4864371 3.028947 0.2060333
    ## Grupo C-Grupo B 0.5675837 -1.0616017 2.196769 0.6913116

- **Respuesta**
  - La comparación de medias para el grupo B y C, empleando el
    procedimiento de Tuckey (HSD) no encuentra diferencias
    significativas (HSD = 0.20, CI95%\[-1.10, 1.50\], p = .93)

# BONUS: Ejercicio 12. Regresión múltiple para comparar los promedios de cada grupo contra el promedio general

En en este ejericio, vamos a ilustrar como emplear a una regresion, para
realizar una prueba t de una sola muestra. En diferentes clases, hemos
indicado, como regresion es una herramienta muy versatil. Este es un
ejemplo de esta versatilidad.

Vamos a crear un modelo de regresión, que nos sirve para comparar si la
pertenencia a alguna de los tipo de escuela, publica, subvencionada, y
particular se diferencia de forma relevante de la media total de los
datos.

Para estos propositos, vamos a crear un modelo de regresion donde:

- Las pruebas de hipótesis de cada media estimada este evaluando si esta
  es distinta del promedio global (esto es basicamente una prueba t de
  una sola muestra).
- El modelo ajustado nos va a peritir estimar las distancias de las
  medias respecto al promedio global de forma simultánea.

``` r
# -----------------------------------------------
# informacion de la variable adm
# -----------------------------------------------

# Dependencia del establecimiento (3 grupos)

# [1] Municipal y AD
# [2] Subvencionado
# [3] Particular

# -----------------------------------------------
# media de los datos
# -----------------------------------------------

dep_center <- mean(data_model$dep, na.rm = TRUE)
dep_center
```

    ## [1] 12

``` r
# -----------------------------------------------
# regresion sobre datos centrados
# -----------------------------------------------

lm((dep-dep_center) ~ -1 + as.factor(adm), data = data_model) %>%
summary()
```

    ## 
    ## Call:
    ## lm(formula = (dep - dep_center) ~ -1 + as.factor(adm), data = data_model)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -11.7178  -4.7178  -0.7178   3.7755  21.7755 
    ## 
    ## Coefficients:
    ##                 Estimate Std. Error t value Pr(>|t|)
    ## as.factor(adm)1  -0.2822     0.4413  -0.639    0.523
    ## as.factor(adm)2   0.2245     0.4007   0.560    0.576
    ## as.factor(adm)3   0.1818     1.8911   0.096    0.923
    ## 
    ## Residual standard error: 6.272 on 455 degrees of freedom
    ##   (42 observations deleted due to missingness)
    ## Multiple R-squared:  0.001606,   Adjusted R-squared:  -0.004977 
    ## F-statistic: 0.244 on 3 and 455 DF,  p-value: 0.8656

``` r
# -----------------------------------------------
# aprovechando la regresion para obtener las medias
# -----------------------------------------------

lm((dep-dep_center) ~ -1 + as.factor(adm), data = data_model) %>%
broom::tidy() %>%
mutate(dep_mean = estimate + dep_center) %>%
knitr::kable(., digits = 2)
```

| term            | estimate | std.error | statistic | p.value | dep_mean |
|:----------------|---------:|----------:|----------:|--------:|---------:|
| as.factor(adm)1 |    -0.28 |      0.44 |     -0.64 |    0.52 |    11.72 |
| as.factor(adm)2 |     0.22 |      0.40 |      0.56 |    0.58 |    12.22 |
| as.factor(adm)3 |     0.18 |      1.89 |      0.10 |    0.92 |    12.18 |

``` r
# -----------------------------------------------
# demostracion 1: medias de los grupos
# -----------------------------------------------

data_model %>%
group_by(adm) %>%
summarize(
mean_dep = mean(dep, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| adm | mean_dep |
|----:|---------:|
|   1 |    11.72 |
|   2 |    12.22 |
|   3 |    12.18 |

``` r
# -----------------------------------------------
# demostracion 2: prueba t de una sola muestra
# -----------------------------------------------

dep_adm_1 <-  data_model %>%
              dplyr::filter(adm == 1) %>%
              dplyr::select(dep)

t.test(dep_adm_1, mu = dep_center, alternative = "two.sided")
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  dep_adm_1
    ## t = -0.63558, df = 201, p-value = 0.5258
    ## alternative hypothesis: true mean is not equal to 12
    ## 95 percent confidence interval:
    ##  10.84239 12.59325
    ## sample estimates:
    ## mean of x 
    ##  11.71782

``` r
dep_adm_2 <-  data_model %>%
              dplyr::filter(adm == 2) %>%
              dplyr::select(dep)

t.test(dep_adm_2, mu = dep_center, alternative = "two.sided")
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  dep_adm_2
    ## t = 0.56389, df = 244, p-value = 0.5733
    ## alternative hypothesis: true mean is not equal to 12
    ## 95 percent confidence interval:
    ##  11.44032 13.00866
    ## sample estimates:
    ## mean of x 
    ##  12.22449

``` r
dep_adm_3 <-  data_model %>%
              dplyr::filter(adm == 3) %>%
              dplyr::select(dep)

t.test(dep_adm_3, mu = dep_center, alternative = "two.sided")
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  dep_adm_3
    ## t = 0.092868, df = 10, p-value = 0.9278
    ## alternative hypothesis: true mean is not equal to 12
    ## 95 percent confidence interval:
    ##   7.819524 16.544112
    ## sample estimates:
    ## mean of x 
    ##  12.18182

> Nota: tambien se puede hacer que un modelo de regresion (uno mas
> complejo), se comporte como una prueba t para muestras dependientes,
> pero con más pasos (ver:
> <https://stats.stackexchange.com/questions/352285/paired-data-comparison-regression-or-paired-t-test/352478#352478>)
