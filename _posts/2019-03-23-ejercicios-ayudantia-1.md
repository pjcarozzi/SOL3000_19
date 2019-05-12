---
title: "Ejercicios ayudantia 1"
categories: ejercicios
---

Utilizando la base de datos [data\_casen\_2017\_1p](https://www.dropbox.com/s/8fo5oebnzdxtoxe/data_casen_2017_1prc.dta?dl=0 "Casen 2017"):

Pregunta 1. Recodificar la variable _edad_ por tramos (_tedad_), que contemple los tramos: 0-14; 15-19; 20-24;25-34; 35-44; 45-54; 55-64; 65 y más.

<details>

  <summary markdown="span"><code>codigo</code></summary>

```
codebook edad
gen tedad1=1 	if edad>=0 & edad <=14
replace tedad1=2 if edad>=15 & edad <=19
replace tedad1=3 if edad>=20 & edad <=24
replace tedad1=4 if edad>=25 & edad <=34
replace tedad1=5 if edad>=35 & edad <=44
replace tedad1=6 if edad>=45 & edad <=54
replace tedad1=7 if edad>=55 & edad <=64
replace tedad1=8 if edad>=65
replace tedad1=. if edad==.
tab tedad1
label variable tedad1 "Tramos edad"
label define etramos 1"0-14" 2"15-19" 3"20-24" 4"25-34" 5"35-44" 6"45-54" 7"55-64" 8"65 y mas"
label values tedad1 etramos
tab tedad1, m

/* Alternativamente */
gen tedad1=edad
recode tedad1 (0/14=1) (15/19=2) (20/24=3) (25/34=4) (35/44=5) (45/54=6) (55/64=7) (65/110=8)
replace tedad1=. if edad==.
label variable tedad1 "Tramos edad"
label values tedad1 etramos
tab tedad1, m
```
</details>

Pregunta 2. Recodificar la variable _educ_ en una nueva variable (llamada _neduc_), que tenga los siguientes atributos:
- S/E Básica incomp. (educ= sin educ, básica incompleta),
- Básica completa (educ= básica completa, media humanista incompleta, media técnica incompleta),
- Media completa (educ= media humanista completa, media técnica completa, técnico superior incompleta, profesional incompleta),
- Técnico superior completa,
- Profesional completa(educ= profesional completa, postgrado incompleto, postgrado completo)

Deje ns/nr como casos perdidos.

<details>

  <summary markdown="span"><code>codigo</code></summary>

```
codebook educ
labelbook educ
tab educ, m
g neduc=0 if educ==0 | educ==1
replace neduc=1 if educ==2 | educ==3 | educ==4
replace neduc=2 if educ==5 | educ==6 | educ==7 | educ==9
replace neduc=3 if educ==8
replace neduc=4 if educ==11 | educ==10 | educ==12
replace neduc=. if educ==99
label variable neduc "Máx. nivel de educación completado
label define neduc 0"S/ed B.I." 1"Básica" 2"Media" 3"Sup.Tec." 4"Sup.Prof." 
label values neduc neduc
tab neduc, m
```
</details>

Pregunta 3. Usando tab y qualifiers, cree tablas univariadas para la variable _neduc_ por sexo para quienes tienen entre 30 y 65 años.

<details>

  <summary markdown="span"><code>codigo</code></summary>

```
bysort sexo: tab neduc if edad>=30 & edad <=65
```
</details>

Pregunta 4. Recodifique _ecivil_ en una variable nueva (_reccivil_) que tenga los siguientes atributos:
- Casado / conviviente
- Anulado, separado, divorciado, viudo
- Soltero

<details>

  <summary markdown="span"><code>codigo</code></summary>

```
codebook ecivil
labelbook ecivil
tab ecivil, m
g reccivil=ecivil
recode reccivil (1/3=1) (4/7=2) (8=3)
label variable reccivil "Estado civil recod."
label define reccivil 1"Casado/conviviente" 2"Anu/sep/div/viu" 3"Soltero"
label values reccivil reccivil
tab reccivil, m
```
</details>

Pregunta 5. Utilizando la variable _asiste_, señale ¿Qué porcentaje de la muestra asiste a un establecimiento educacional?

<details>

  <summary markdown="span"><code>codigo</code></summary>

```
tab asiste, m
```
</details>

Pregunta 6. Utilizando la variable _depen_, genere una tabla univariada que dé cuenta de la distribución de porcentajes por dependencia educacional entre quienes asisten a unestablecimiento educacional. Recodifique antes NS/NR como caso perdido. ¿Cuál es la moda? ¿Qué porcentaje de la muestra asiste a una universidad del CRUCH?

<details>

  <summary markdown="span"><code>codigo</code></summary>

```
tab depen, m
codebook depen
labelbook depen
replace depen=. if depen==99
tab depen if asiste==1
```
</details>

Pregunta 7. Genere tablas univariadas que le permitan comparar la distribución por dependencia educacional y zona de residencia entre quienes tienen 17 años o menos. Interprete los resultados.

<details>

  <summary markdown="span"><code>codigo</code></summary>

```
bysort zona: tab depen if edad<=17
bysort depen: tab zona if edad<=17 & depen!=.
```
</details>

