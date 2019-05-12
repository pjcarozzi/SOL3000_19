<p>Los qualifiers y operadores son una parte importante del lenguaje de Stata. Revisaremos el qualifier <code>in</code>, el qualifier <code>if</code> y el prefijo <code>by</code>.</p>
<h2 id="qualifier-in">Qualifier in</h2>
<p><code>in</code> permite que un determinado comando se ejecute usando solo las observaciones especificadas en un rango. Los rangos se identifican de la siguente manera:</p>
<table>
<thead>
<tr class="header">
<th>Exp</th>
<th>Descripcion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>X</td>
<td>La Xva observacion</td>
</tr>
<tr class="even">
<td>X/Y</td>
<td>Rango entre la Xva observacion y la Yva observacion</td>
</tr>
<tr class="odd">
<td>X/l</td>
<td>Rango entre la Xva observacion y la ultima observacion (last)</td>
</tr>
<tr class="even">
<td>f/X</td>
<td>Rango entre la primera observacion (first) y la Xva observacion</td>
</tr>
</tbody>
</table>
<p>Obtengamos la media de escolaridad para las primeras 100 observaciones.</p>
<pre class='stata'>. summarize esc in f/100

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │         78    11.98718    3.701504          0         21
</pre>
<h2 id="qualifier-if">Qualifier if</h2>
<p><code>if</code> permite que el comando en cuestion se ejecute solo en las observaciones que cumplen con una expresion determinada, condicional a los valores de otra variable.</p>
<p>Las expresiones utilizan operadores:</p>
<table>
<thead>
<tr class="header">
<th>Operadores relacionales</th>
<th>Operadores matematicos</th>
<th>Operadores logicos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>&gt; Mayor que</td>
<td>+ Adicion</td>
<td>&amp; Y</td>
</tr>
<tr class="even">
<td>&lt; Menor que</td>
<td>- Sustraccion</td>
<td></td>
</tr>
<tr class="odd">
<td>&gt;= Mayor o igual que</td>
<td>* Multiplicacion</td>
<td>! No</td>
</tr>
<tr class="even">
<td>&lt;= Menor o igual que</td>
<td>/ Division</td>
<td></td>
</tr>
<tr class="odd">
<td>== Igual</td>
<td>^ Potencia</td>
<td></td>
</tr>
<tr class="even">
<td>!= No igual</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>
<p>Obtengamos la media de escolaridad entre las mujeres mayores de 60 años. Primero veamos como se codifica mujer en la base de datos:</p>
<pre class='stata'>. codebook sexo

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
sexo                                                                                                                                                                       Sexo
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

                  type:  numeric (double)
                 label:  sexo
    
                 range:  [1,2]                        units:  1
         unique values:  2                        missing .:  0/2,164
    
            tabulation:  Freq.   Numeric  Label
                         1,038         1  Hombre
                         1,126         2  Mujer
</pre>
<p>Observamos que, en las etiquetas de valores, “hombre” esta codificado como “1” y “mujer” como “2”. Calculamos la media de escolaridad para las mujeres que tienen 60 años o mas en la muestra, usando qualifiers y operadores.</p>
<pre class='stata'>. summarize esc if sexo==2 &amp; edad>=60

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │        243    7.683128    4.826152          0         19
</pre>
<h2 id="prefijo-by">Prefijo by</h2>
<p><code>by</code> permite ejecutar un comando de manera separada para grupos de observaciones identificados con un valor determinado en una variable. Es util para analizar subsets de datos.</p>
<p>Supongamos que queremos calcular la media de escolaridad por sexo. Para ello, ejecutaremos <code>summarize</code> de manera separada para quienes comparten el valor “1”, los hombres, y quienes comparten el valor “2”, las mujeres.</p>
<p>Para poder computarlo, <code>by</code> requiere que las observaciones esten ordenadas segun la variable que identifica los grupos. En este caso, que en la lista de observaciones aparezcan primero los hombres y luego las mujeres.</p>
<p>Usamos el comando <code>sort</code> previamente, y luego <code>summarize</code>.</p>
<pre class='stata'>. sort sexo

. by sexo: summarize esc

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
-> sexo = Hombre

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │        821    11.01218    4.077882          0         22

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
-> sexo = Mujer

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │        928    10.85022    4.408996          0         21
</pre>
<p>La media de escolaridad para los hombres es 11 años y para las mujeres, 10,9 años.</p>
<p>Podemos evitar el paso previo de ordenar las variables usando <code>bysort</code>. Reordenemos las observaciones por folio.</p>
<pre class='stata'>. sort folio

. list sexo in 1/10

     ┌────────┐
     │   sexo │
     ├────────┤
  1. │  Mujer │
  2. │ Hombre │
  3. │  Mujer │
  4. │ Hombre │
  5. │ Hombre │
     ├────────┤
  6. │ Hombre │
  7. │  Mujer │
  8. │ Hombre │
  9. │ Hombre │
 10. │ Hombre │
     └────────┘
</pre>
<p>Podemos ver que las observaciones ya no estan ordenadas por sexo. Si intentamos ejecutar el comando que acabamos de usar para calcular las medias, el output nos mostrara un error.</p>
<pre class='stata'>. by sexo: summarize esc
  not sorted
  r(5);
</pre>
<p>Si hacemos click en el link r(5), se abrira la ventana de visor detallando una busqueda que entrega informacion respecto al error que cometimos.</p>
<p>Usemos <code>bysort</code>.</p>
<pre class='stata'>. bysort sexo: summarize esc

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
-> sexo = Hombre

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │        821    11.01218    4.077882          0         22

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
-> sexo = Mujer

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │        928    10.85022    4.408996          0         21
</pre>
<p>Los resultados que aparecen en el output son exactamente iguales a los obtenidos al ordenar previamente las observaciones.</p>
<p>El prefijo <code>by</code> no puede ser utilizado en forma conjunta con el qualifier <code>in</code>, pero si acepta el uso del qualifier <code>if</code>.</p>
<p>Obtengamos la media de escolaridad por zona de residencia (urbana o rural) para las observaciones que tienen 45 años o mas y son mujeres.</p>
<pre class='stata'>. bysort zona: summarize esc if edad>=45 &amp; sexo==2

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
-> zona = Urbano

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │        389    9.532134    4.643155          0         21

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
-> zona = Rural

    Variable │        Obs        Mean    Std. Dev.       Min        Max
─────────────┼─────────────────────────────────────────────────────────
         esc │         85    6.976471    4.011817          0         17
</pre>
<p>En esta muestra, las mujeres de 45 años o mas que viven en una zona urbana tienen en promedio 9. años de escolaridad, mientras que las mujeres de 45 años o mas que viven en una zona rural tienen en promedio 6.8 años de escolaridad.</p>
