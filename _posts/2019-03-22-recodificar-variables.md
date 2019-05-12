<h2 id="variables-y-etiquetas">Variables y etiquetas</h2>
<p>Volvamos a revisar las variables presentes en la base de datos.</p>
<pre class='stata'>. describe

Contains data from data/data_casen_2017_1p.dta
  obs:         2,164
 vars:            29                          21 March 2019 23:53
 size:       502,048
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
              storage   display    value
variable name   type    format     label      variable label
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
folio           double  %10.0g                Identificacion hogar (comuna area seg viv hogar)
o               double  %10.0g                Orden
id_vivienda     double  %10.0g                Identificador de la vivienda (comuna area seg viv)
hogar           double  %10.0g                Identificacion del hogar en la vivienda
region          double  %49.0g     region     Region
provincia       double  %23.0g     provincia
                                              Provincia
comuna          double  %10.0g     comuna     Comuna
zona            double  %10.0g     zona       Zona
expr            double  %10.0g                Factor de Expansion Regional
expc            double  %10.0g                Factor de Expansion Comunal
expr_div        double  %10.0g                Factor de expansion orientacion sexual (r23) e identidad de genero (r24)
varstrat        double  %10.0g                Estratos de Varianza
varunit         double  %10.0g                Conglomerados de Varianza
sexo            double  %10.0g     sexo       Sexo
edad            double  %10.0g                Edad
ecivil          double  %47.0g     ecivil     Estado civil
o1              double  %19.0g     DICO       o1. La semana pasada, trabajo al menos una hora, sin considerar los quehaceres
o2              double  %19.0g     DICO       o2. Aunque no trabajo la semana pasada, realizo alguna actividad por lo menos d
o3              double  %19.0g     DICO       o3. Aunque no trabajo la semana pasada, tenia algun empleo, negocio u otra acti
o6              double  %19.0g     DICO       o6. Busco trabajo remunerado o realizo alguna gestion para iniciar una activida
oficio1         double  %60.0g     oficio1    o9a_cod. Cual es su ocupacion u oficio? (1 digito)
ytotcorh        double  %10.0g                Ingreso total del hogar corregido
ypc             double  %10.0g                Ingreso total per capita del hogar corregido
numper          double  %10.0g                Numero de personas en el hogar (excluye sdpa)
asiste          double  %10.0g     asiste     Asiste
esc             double  %10.0g                Escolaridad
educ            double  %33.0g     educ       Nivel Educacional
depen           double  %48.0g     depen      Dependencia Administrativa
activ           double  %10.0g     activ      Condicion de actividad
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Sorted by: zona
</pre>
<p>Stata tiene distintas formas de identificar una variable:</p>
<ul>
<li><em>Variable name</em>. El nombre de la variable, que por conveniencia suele mantenerse corto para facilitar su uso mediante comandos.</li>
<li><em>Variable label</em>. La etiqueta de la variable, lo que describe a la variable. Si una variable tiene etiqueta, este sera el nombre que aparece en las tablas y graficos, entre otros.</li>
<li><em>Value label</em>. El nombre de la etiqueta de valores que contiene los nombres de los atributos de la variable. Las variables continuas no suelen estar asociadas a una etiqueta de valores, pero estos son utiles para identificar los atributos de las variables categoricas.</li>
</ul>
<p><code>codebook</code> y <code>labelbook</code> nos permiten conocer estos identificadores.</p>
<p><code>codebook</code> examina los nombres y etiquetas de las variables. Si no especificamos ninguna variable junto el comando, <code>codebook</code> nos muestra informacion para todas las variables en la base de datos. Tambien podemos ejecutar el comando seguido de una variable o lista de variables.</p>
<p>Exploremos la ocupacion u oficio de los casos en la muestra.</p>
<pre class='stata'>. codebook oficio1

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
oficio1                                                                                                                      o9a_cod. Cual es su ocupacion u oficio? (1 digito)
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

                  type:  numeric (double)
                 label:  oficio1

                 range:  [0,999]                      units:  1
         unique values:  11                       missing .:  1,206/2,164

              examples:  5     Trabajadores de los servicios y vendedores de comerci
                         9     Trabajadores no calificado
                         .
                         .
</pre>
<p>Podemos observar que la variable oficio1 es una variable categorica, con un rango de atributos que va del 0 al 999. Cuando las variables poseen muchos atributos (etiquetados), <code>codebook</code> no muestra sino parte de ellos, como en este caso.</p>
<p>Si queremos ver todos los atributos etiquetados asociados a las variable, usamos el comando <code>labelbook</code>.</p>
<p><code>labelbook</code>, a diferencia de <code>codebook</code>, no se refiere a las variables en si, sino a las etiquetas de variables, que son registradas en Stata como informacion independiente. Varias variables pueden compartir una etiqueta de variables.</p>
<p>Debido a esto, necesitamos identificar previamente el nombre de la etiqueta de variables que esta asociada a la variable de interes. El output de <code>codebook</code> nos muestra esta informacion. En este caso, la etiqueta de variable de <code>oficio1</code> tambien se llama <code>oficio1</code>.</p>
<p>Si ejecutamos <code>labelbook</code> sin especificaciones, se desplegara el libro de etiquetas completo. Nuevamente, si ejecutamos <code>labelbook</code> seguido por una etiqueta de variable o una lista de etiquetas de variables, nos mostrara los atributos etiquetados solo para estas etiquetas.</p>
<pre class='stata'>. labelbook oficio1

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
value label oficio1
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

      values                                    labels
       range:  [0,999]                   string length:  [8,60]
           N:  11                unique at full length:  yes
        gaps:  yes                 unique at length 12:  no
  missing .*:  0                           null string:  no
                               leading/trailing blanks:  no
                                    numeric -> numeric:  no
  definition
           0   Fuerzas Armada
           1   Miembros del poder ejecutivo y de los cuerpos legislativo
           2   Profesionales, cientificos e intelectuale
           3   Tecnicos profesionales de nivel medi
           4   Empleados de oficina
           5   Trabajadores de los servicios y vendedores de comerci
           6   Agricultores y trabajadores calificados agropecuarios y pesq
           7   Oficiales, operarios y artesanos de artes mecanicas y de otr
           8   Operadores de instalaciones y maquinas y montadore
           9   Trabajadores no calificado
         999   Sin dato

   variables:  oficio1
</pre>
<p>Podemos ver que, si bien el rango de valores de <em>oficio1</em> va de 0 a 999, no todos los valores estan etiquetados. El valor 999 corresponde a “Sin dato”. En este caso, la etiqueta de valores <code>oficio1</code> solo es usada por la variable <code>oficio1</code>.</p>
<p>Revisemos otra etiqueta de valores:</p>
<pre class='stata'>. labelbook DICO

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
value label DICO
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

      values                                    labels
       range:  [1,9]                     string length:  [2,19]
           N:  3                 unique at full length:  yes
        gaps:  yes                 unique at length 12:  yes
  missing .*:  0                           null string:  no
                               leading/trailing blanks:  no
                                    numeric -> numeric:  no
  definition
           1   Si
           2   No
           9   No sabe/no responde

   variables:  o1 o2 o3 o6
</pre>
<p>La etiqueta de valores <em>DICO</em>, definida como 1 “si”, 2 “no”, 9 “no sabe/no responde”, es compartida por las variables <code>o1</code>, <code>o2</code>, <code>o3</code> y <code>o6</code>.</p>
<h2 id="recodificaciones">Recodificaciones</h2>
<p>Identificar previamente el nivel de medicion y los atributos de las variables es necesario a la hora de recodificar variables, o crear variables a partir de las existentes.</p>
<p>Dos comandos basicos que permiten generar/recodificar datos son <code>generate</code> y <code>replace</code>.</p>
<p><code>generate</code>, abreviado <code>gen</code> o <code>g</code>, nos permite crear una nueva variable especificando su nombre y una expresion que determinara su contenido.</p>
<p>Creemos una variable llamada <code>varnueva</code> en la cual todas las observaciones compartan el valor 1.</p>
<pre class='stata'>. gen varnueva=1
</pre>
<pre class='stata'>. list varnueva in 1/5

     ┌──────────┐
     │ varnueva │
     ├──────────┤
  1. │        1 │
  2. │        1 │
  3. │        1 │
  4. │        1 │
  5. │        1 │
     └──────────┘
</pre>
<p><code>replace</code> cambia el contenido de una variable existente.</p>
<p>Reemplacemos el contenido de <code>varnueva</code> indicando que todas las observaciones tengan el valor 7</p>
<pre class='stata'>. replace varnueva=7
(2,164 real changes made)
</pre>
<pre class='stata'>. list varnueva in 1/5

     ┌──────────┐
     │ varnueva │
     ├──────────┤
  1. │        7 │
  2. │        7 │
  3. │        7 │
  4. │        7 │
  5. │        7 │
     └──────────┘
</pre>
<p>Eliminemos <code>varnueva</code></p>
<pre class='stata'>. drop varnueva
</pre>
<p>Los qualifiers y operadores que ya revisamos nos permitiran recodificar variables. Usemos operadores aritmeticos para calcular el ingreso total per capita para cada observacion de la muestra, creando una variable que se llamara <code>ypcapita</code>.</p>
<p>Utilizaremos dos variables existentes: <code>ytotcorh</code>, el ingreso total del hogar, y <code>numper</code>, el numero de personas en el hogar.</p>
<pre class='stata'>. gen ypcapita=ytotcorh/numper
(2 missing values generated)
</pre>
<p>Revisemos los estadisticos descriptivos para el ingreso total per capita.</p>
<pre class='stata'>. summarize ypcapita

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
    ypcapita │      2,162    357332.5    625617.8          0   2.24e+07
</pre>
<p>La media de ingreso per capita es $357333. La variable <code>ypc</code>, generada por Casen, contiene la misma informacion.</p>
<pre class='stata'>. list ypcapita ypc in f/10

     ┌───────────────────┐
     │ ypcapita      ypc │
     ├───────────────────┤
  1. │ 211154.3   211154 │
  2. │   285000   285000 │
  3. │ 203264.3   203264 │
  4. │ 116666.7   116667 │
  5. │  94511.5    94512 │
     ├───────────────────┤
  6. │   267833   267833 │
  7. │ 330504.8   330505 │
  8. │ 248258.2   248258 │
  9. │ 216666.7   216667 │
 10. │   300000   300000 │
     └───────────────────┘
</pre>
<p>Supongamos que nos encargan calcular el porcentaje de personas en edad de trabajar. Sabemos que, por definicion de Casen, son personas en edad de trabajar todos quienes tienen 15 años o mas.</p>
<p>Construyamos una variable dicotomica que identifique con 1 a quienes tienen 15 años o mas, y con 0 a quienes tienen menos de 15 años.</p>
<p>Primero, verifiquemos si la variable <code>edad</code> tiene valores perdidos o si existe un valor que identifique que la edad no ha sido registrada (ej. NS/NR, 999).</p>
<pre class='stata'>. codebook edad

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
edad                                                                                                                                                                       Edad
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

                  type:  numeric (double)

                 range:  [0,95]                       units:  1
         unique values:  95                       missing .:  0/2,164

                  mean:   37.5457
              std. dev:   22.5719

           percentiles:        10%       25%       50%       75%       90%
                                 7        19        36        55        68
</pre>
<p>La variable no tiene casos perdidos. Tampoco se ha codificado un valor tal que nos sugiera dejar fuera algunos casos para los que no existe el dato.</p>
<p>Usamos la variable <code>edad</code>, tal y como es codificada en Casen, y el qualifier <code>if</code> para crear una nueva variable llamada <code>pet</code>.</p>
<pre class='stata'>. gen pet=0

. replace pet=1 if edad>=15
(1,760 real changes made)
</pre>
<p><code>recode</code> es otro comando que podemos usar para cumplir con esta tarea. <code>recode</code> cambia los valores numericos de una variable de acuerdo con reglas especificas.</p>
<p>Esta vez usaremos rangos de edad:</p>
<pre class='stata'>. gen pet2=edad

. recode pet2 (0/14=0) (15/95=1)
(pet2: 2143 changes made)
</pre>
<p>Ambas maneras nos entregan los mismos resultados. Corroboremos si la cantidad de personas en edad de trabajar es igual bajo ambas recodificaciones. Utilizamos el comando <code>tabulate</code>, abreviado <code>tab</code>, para obtener tablas de frecuencias y porcentajes. Podemos escribir, en dos pasos:</p>
<pre class='stata'>. tab pet

        pet │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
          0 │        404       18.67       18.67
          1 │      1,760       81.33      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00

. tab pet2

       pet2 │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
          0 │        404       18.67       18.67
          1 │      1,760       81.33      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00
</pre>
<p>O en sólo uno:</p>
<pre class='stata'>. tab1 pet pet2

-> tabulation of pet

        pet │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
          0 │        404       18.67       18.67
          1 │      1,760       81.33      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00

-> tabulation of pet2

       pet2 │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
          0 │        404       18.67       18.67
          1 │      1,760       81.33      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00
</pre>
<p>Ambas tablas muestran que tenemos 1760 personas en edad de trabajar, lo que equivale a un 81.33% de nuestra muestra.</p>
<p>Supongamos ahora que nos encargan identificar la condicion de actividad de los encuestados, con el fin de calcular las tasas de ocupacion, desocupacion e inactividad.</p>
<p>Primero necesitamos identificar las variables que nos sirven para construir la variable que identifique en la muestra a quienes estan ocupados, desocupados e inactivos. La siguiente figura muestra un fragmento del Modulo Trabajo del <a href="http://observatorio.ministeriodesarrollosocial.gob.cl/casen-multidimensional/casen/docs/Cuestionario_Casen2017.pdf">Cuestionario Casen 2017</a> y sintetiza la logica que seguiremos en nuestra recodificacion.</p>
<figure>
<center>
<img src="https://raw.githubusercontent.com/pjcarozzi/SOL3000_19/master/_posts/img/a1_4_fig1.jpg" alt="recod" /><figcaption>Figura 1. Preguntas y filtros</figcaption>
</center>
</figure>
<p>Generamos tablas de frecuencia para las variables que necesitamos usando <code>tab1</code> con la opcion missing (abreviada m). La opción missing nos permite tratar los datos perdidos como si fueran una categoría adicional y saber cual es su porcentaje en la muestra</p>
<pre class='stata'>. tab1 o1 o2 o3 o6, m

-> tabulation of o1

      o1. La semana │
 pasada, trabajo al │
menos una hora, sin │
     considerar los │
         quehaceres │      Freq.     Percent        Cum.
────────────────────┼───────────────────────────────────
                 Si │        920       42.51       42.51
                 No │        840       38.82       81.33
                  . │        404       18.67      100.00
────────────────────┼───────────────────────────────────
              Total │      2,164      100.00

-> tabulation of o2

      o2. Aunque no │
  trabajo la semana │
    pasada, realizo │
   alguna actividad │
     por lo menos d │      Freq.     Percent        Cum.
────────────────────┼───────────────────────────────────
                 Si │         13        0.60        0.60
                 No │        827       38.22       38.82
                  . │      1,324       61.18      100.00
────────────────────┼───────────────────────────────────
              Total │      2,164      100.00

-> tabulation of o3

      o3. Aunque no │
  trabajo la semana │
pasada, tenia algun │
  empleo, negocio u │
          otra acti │      Freq.     Percent        Cum.
────────────────────┼───────────────────────────────────
                 Si │         25        1.16        1.16
                 No │        802       37.06       38.22
                  . │      1,337       61.78      100.00
────────────────────┼───────────────────────────────────
              Total │      2,164      100.00

-> tabulation of o6

  o6. Busco trabajo │
       remunerado o │
     realizo alguna │
       gestion para │
        iniciar una │
           activida │      Freq.     Percent        Cum.
────────────────────┼───────────────────────────────────
                 Si │         89        4.11        4.11
                 No │        713       32.95       37.06
                  . │      1,362       62.94      100.00
────────────────────┼───────────────────────────────────
              Total │      2,164      100.00
</pre>
<p>En <code>o1</code> tenemos 404 casos perdidos. Esto se explica porque las preguntas de <code>o1</code> a <code>o8</code> solo son contestadas por quienes tienen 15 años o mas. Podemos comprobarlo al ejecutar:</p>
<pre class='stata'>. tab o1 if edad&lt;15, m

      o1. La semana │
 pasada, trabajo al │
menos una hora, sin │
     considerar los │
         quehaceres │      Freq.     Percent        Cum.
────────────────────┼───────────────────────────────────
                  . │        404      100.00      100.00
────────────────────┼───────────────────────────────────
              Total │        404      100.00
</pre>
<p>A las variables <code>o1</code>, <code>o3</code> y <code>o6</code> se le suman como casos perdidos quienes han respondido “si” en las preguntas anteriores.</p>
<pre class='stata'>. dis 404+920
1324

. dis 1324+13
1337

. dis 1337+25
1362
</pre>
<p>Creamos una variable nueva, llamada <code>act</code>, que sea condicional a los valores de <code>o1</code>, <code>o2</code>, <code>o3</code> y <code>o6</code>, usando el qualifier <code>if</code>.</p>
<p><code>act</code> es igual a 1 si el o la encuestada contesto <code>o1</code> u <code>o2</code> u <code>o3</code> con “si”, por lo tanto, se encuentra ocupado/a.</p>
<pre class='stata'>. gen act=1 if o1==1 | o2==1 | o3==1
(1,206 missing values generated)
</pre>
<p>Esto genera 1206 casos pedidos para los que la expresion logica no se cumple. Reemplazamos parte de esos casos perdidos con “2” si el o la encuestada responde “si” en la pregunta <code>o6</code>, por lo tanto, se encuentra desocupado.</p>
<pre class='stata'>. replace act=2 if o6==1
(89 real changes made)
</pre>
<p>Son reemplazados 82 casos para los cuales si se cumplia <code>o6==1</code>. Finalmente, nos queda definir a quienes respondieron “no” en <code>o6</code>. Alternativamente, podemos usar el operador <code>!=</code> y condicionar el remplazo a quienes no respondieron “si” en las preguntas anteriores, dejando como perdidos a quienes no son poblacion en edad de trabajar (el resultado es el mismo)-</p>
<pre class='stata'>. replace act=3 if o1!=1 &amp; o2!=1 &amp; o3!=1 &amp; o6!=1
(1,117 real changes made)

. replace act=. if pet==0
(404 real changes made, 404 to missing)
</pre>
<p>Comparamos la variable recien creada tabulando <code>act</code> y <code>activ</code>, variable creada por Casen que contiene la misma informacion.</p>
<pre class='stata'>. tab1 act activ, m

-> tabulation of act

        act │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
          1 │        958       44.27       44.27
          2 │         89        4.11       48.38
          3 │        713       32.95       81.33
          . │        404       18.67      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00

-> tabulation of activ

  Condicion │
         de │
  actividad │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
   Ocupados │        958       44.27       44.27
Desocupados │         89        4.11       48.38
  Inactivos │        713       32.95       81.33
          . │        404       18.67      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00
</pre>
<p>O como tabla cruzada</p>
<pre class='stata'>. tab act activ, m

           │           Condicion de actividad
       act │  Ocupados  Desocupad  Inactivos          . │     Total
───────────┼────────────────────────────────────────────┼──────────
         1 │       958          0          0          0 │       958
         2 │         0         89          0          0 │        89
         3 │         0          0        713          0 │       713
         . │         0          0          0        404 │       404
───────────┼────────────────────────────────────────────┼──────────
     Total │       958         89        713        404 │     2,164
</pre>
<p>Nos falta identificar la variable <code>act</code> y sus atributos. Primero creamos una etiqueta de variable que la describa-</p>
<pre class='stata'>. label variable act "Actividad"
</pre>
<p>Si queremos usar otra etiqueta, simplemente sobreescribimos.</p>
<pre class='stata'>. label variable act "Actividad recodificada"
</pre>
<p>Ahora etiquetemos los atributos. Primero debemos definir una etiqueta de valores y parear cada valor con el atributo que queremos que muestre.</p>
<pre class='stata'>. label define valactividad 1 "Ocupado" 2 "Desempleado" 3 "Inactivo"
</pre>
<p>Si queremos cambiar algun valor o etiqueta de valor, usamos la opcion <code>replace</code>.</p>
<pre class='stata'>. label define valactividad 1 "Ocupado" 2 "Desocupado" 3 "Inactivo", replace
</pre>
<p>Si queremos agregar un valor y su etiqueta, usamos la opcion <code>add</code>.</p>
<pre class='stata'>. label define valactividad 9 "No PET", add
</pre>
<p>El segundo paso es enlazar la variable a la etiqueta de valores creada.</p>
<pre class='stata'>. label values act valactividad
</pre>
<p>Tabulemos la variable <code>act</code>.</p>
<pre class='stata'>. tab act, m

  Actividad │
recodificad │
          a │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
    Ocupado │        958       44.27       44.27
 Desocupado │         89        4.11       48.38
   Inactivo │        713       32.95       81.33
          . │        404       18.67      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00
</pre>
<p>Las etiquetas de valores no modifican los valores de las variables. En este caso, definimos una etiqueta para el valor “9” como “No PET”, pero este no existe en la variable, por lo que simplemente no los muestra.</p>
<p>Recodifiquemos a quienes no son poblacion en edad de trabajar como “9”.</p>
<pre class='stata'>. replace act=9 if pet==0
(404 real changes made)
</pre>
<p>Veamos ahora la tabla de frecuencias de <code>act</code>.</p>
<pre class='stata'>. tab act, m

  Actividad │
recodificad │
          a │      Freq.     Percent        Cum.
────────────┼───────────────────────────────────
    Ocupado │        958       44.27       44.27
 Desocupado │         89        4.11       48.38
   Inactivo │        713       32.95       81.33
     No PET │        404       18.67      100.00
────────────┼───────────────────────────────────
      Total │      2,164      100.00
</pre>
<h2 id="guardar-los-cambios-en-la-base-de-datos">Guardar los cambios en la base de datos</h2>
<p>Para guardar la base de datos modificada, usamos:</p>
<pre class='stata'>. save data_casen_ayud1, replace
(note: file data_casen_ayud1.dta not found)
file data_casen_ayud1.dta saved
</pre>
<p>Si estamos usando un <code>log file</code>, lo cerramos usando su nombre:</p>
<pre class='stata'>. *log close ayudantia
</pre>
