<h4 align="center"> 
M2 ECAP <br> 
</h4>

<h3 align="center" style="font-size: 28px;">
Projet de Machine Learning : <br>
Le cas des haricots secs
</h3>

<h4 align="center"> 
Cassandre ORHAN & Marie KERHOAS <br> <br>
Mai 2025<br><br><hr>
</h4>

## Introduction

Le sujet de notre étude concerne les haricots secs. Nous disposons d'une base de données répertoriant 13 611 grains de 7 variétés différentes de haricots secs. De plus, nous avons pour chaque grain des indications sur ses dimensions et sa forme grâce à 16 variables renseignées. Aussi, nous chercherons à mettre en place un modèle de machine learning nous permettant de classer de façon pertinente ces grains dans la variété auquelle ils appartiennent, en nous basant sur leurs caractéristiques observées. Il est à noter que nous avons choisi de nous concentrer sur uniquement deux des variétés de haricots secs afin de réaliser cette étude.

## Analyse exploratoire

### Présentation des variables

Comme nous l'avons évoqué précédemment, nous disposons de 17 variables : celle indiquant la variété du grain ainsi que 16 autres le décrivant. L'ensemble de ces variables explicatives sont quantitatives et nous allons les présenter. Elles ont été obtenues grâce à des photos prises de tous les grains, par un appareil photo à haute résolution,  qui ont ensuite permis d'extraire les caractéristiques de ces grains par ordinateur.


- __Area (A):__ La surface d'une zone de haricots et le nombre de pixels à l'intérieur de ses limites.
- __Perimeter (P):__ La circonférence d'un haricot est définie comme la longueur de sa bordure.
- __Major axis length (L):__ La distance entre les extrémités de la ligne la plus longue qui peut être tracée à partir d'un haricot.
- __Minor axis length (l):__ La ligne la plus longue qui peut être tracée à partir d'un haricot tout en étant perpendiculaire à l'axe principal.
- __Aspect ratio (K):__ Définit la relation entre L et l.
- __Eccentricity (Ec):__ Excentricité de l'ellipse ayant les mêmes moments que la région.
- __Convex area (C):__ Nombre de pixels dans le plus petit polygone convexe pouvant contenir la surface d'une graine de haricot.
- __Equivalent diameter (Ed):__ Le diamètre d'un cercle ayant la même surface qu'une graine de haricot.
- __Extent (Ex):__ Rapport entre les pixels de la boîte englobante et la surface de la graine de haricot.
- __Solidity (S):__ Également appelée convexité. Il s'agit du rapport entre les pixels de la coquille convexe et ceux des haricots.
- __Roundness (R):__ Calculée à l'aide de la formule suivante : (4piA)/(P^2)
- __Compactness (CO):__ Mesure la rondeur d'un objet : Ed/L
- __ShapeFactor1 (SF1)__
- __ShapeFactor2 (SF2)__
- __ShapeFactor3 (SF3)__
- __ShapeFactor4 (SF4)__
- __Class__ (Seker, Barbunya, Bombay, Cali, Dermosan, Horoz and Sira)

Comme on peut le voir, nous ne disposons pas d'informations déscriptives suffisantes sur les 4 ShapeFactors, aussi nous avons choisi de ne pas les prendre en compte.

### Choix des variétés retenues

Etant donné notre choix de nous focaliser sur deux des catégories proposées, nous avons dans un premier temps du les sélectionner. Pour cela, nous avons commencer par observer la répartition des grains entre les classes.

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/8913cb045d7b9301b2b6717a61fe809d0cdef41b/Projet/Images/1.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

Afin de conserver un nombre de lignes conséquent dans notre jeu de données, nous avions le choix entre les 4 variétés suivantes : Dermason, Sira, Seker et Horoz.

Par ailleurs, nous avons également cherché à connaitre la distribution des variétés selon les différentes variables dont nous disposions. 

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/8913cb045d7b9301b2b6717a61fe809d0cdef41b/Projet/Images/2.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

Notre choix s'est alors porté sur 2 variétés semblant présenter des caractéristiques relativement distinctes : Dermason et Horoz.

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/8913cb045d7b9301b2b6717a61fe809d0cdef41b/Projet/Images/Logo_IAE.jpg"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

### Les statistiques descriptives

Afin d'améliorer notre compréhension des données choisies, nous avons calculé leurs principales statistiques descriptives

### Les distribution des caractéristiques selon les 2 variétes

### Les corrélations 

L'étape suivante a consisté à étudier les coefficients des corrélations entre nos variables explicatives.

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/8913cb045d7b9301b2b6717a61fe809d0cdef41b/Projet/Images/Logo_IAE.jpg"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

Dans notre cas, nous avons constaté que des coefficients très importants étaient présents dans la matrice de corrélation obtenue. Cela nous a contraint à exclure 5 des nos variables. 

La seconde matrice de corrélation réalisée après la suppression des colonnes était donc la suivante :

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/8913cb045d7b9301b2b6717a61fe809d0cdef41b/Projet/Images/Logo_IAE.jpg"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>





## 


<div align="center">

| Item         | Price | In stock |
|--------------|:-----:|:--------:|
| Juicy Apples |  1.99 |     739  |
| Bananas      |  1.89 |       6  |

<i>Légende </i>
<br><br>
</div>


<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/8913cb045d7b9301b2b6717a61fe809d0cdef41b/Projet/Images/Logo_IAE.jpg"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

`code`

## Modèles

...

## Conclusion






