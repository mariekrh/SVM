<h4 align="center"> 
M2 ECAP <br> 
</h4>

<h3 align="center" style="font-size: 28px;">
Projet de Machine Learning : <br>
Prédiction de la variété d'haricots secs selon leurs caractéristiques
</h3>

<h4 align="center"> 
Cassandre ORHAN & Marie KERHOAS <br> <br>
Mai 2025<br><br><hr>
</h4>

## Introduction

Le sujet de notre étude concerne les haricots secs. Nous disposons d'une base de données répertoriant 13 611 grains de 7 variétés différentes de haricots secs. De plus, nous avons pour chaque grain des indications sur ses dimensions et sa forme grâce à 16 variables renseignées. Aussi, nous chercherons à mettre en place un modèle de machine learning nous permettant de classer de façon pertinente ces grains dans la variété auquelle ils appartiennent, en nous basant sur leurs caractéristiques observées. Par la suite nous chercherons à l'interpréter de façon globale puis locale. Il est à noter que nous avons choisi de nous concentrer sur uniquement deux des variétés de haricots secs afin de réaliser cette étude.

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
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/1.png"
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
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/2.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

Notre choix s'est alors porté sur 2 variétés semblant présenter des caractéristiques relativement distinctes : Dermason et Horoz. Leur répartition est la suivante :

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/3.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

### Les distribution des caractéristiques selon les 2 variétes

A présent notre choix de variétés fait, nous avons une nouvelle fois réalisé des graphiques présentant la distribution des caractéristiques mais cette fois, seulement selon les variétés Dermason et Horoz.

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/4.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

### Les corrélations 

L'étape suivante a consisté à étudier les coefficients des corrélations entre nos variables explicatives.

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/5.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

Dans notre cas, nous avons constaté que des coefficients très importants étaient présents dans la matrice de corrélation obtenue. Cela nous a contraint à exclure 5 des nos variables : Area, Perimeter, Aspect Ratio, Equivalent diameter et Compactness. La matrice de corrélation réalisée après la suppression des colonnes est donc la suivante :

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/6.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>


### Les outliers

Nous avons par la suite chercher à étudier les possibles valeur atypique et avons pour cela appliqué un test ESD qui permet de détecter automatiquement un ou plusieurs outliers dans une distribution supposée normale en comparant l'écart d'une observation au reste de l'échantillon. 
Le test a révélé que seules les variables Solidity et Roundness présentaient respectivement 100 et 5 valeurs atypiques. Nous avons décidé de ne pas les corriger, car ces variables conservent un pouvoir discriminant (comme le montre la graphique ci-dessous) entre les classes Dermason et Horoz, sans être structurellement perturbées par la présence de quelques valeurs extrêmes.
<!--
![image sur Github](https://github.com/user-attachments/assets/ae43b5f4-f8b0-498b-ab57-7764eb0f5c91)
-->


<br>

<div align="center">
  <img 
  src="https://github.com/user-attachments/assets/ae43b5f4-f8b0-498b-ab57-7764eb0f5c91"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>


### Le resample

Par la suite, nous avons choisi de rééquilibrer nos données en utilisant un resample. Cela nous a permis d'effectuer une sélection parmi les grains de la variété Dermason afin d'en conserver autant que ceux disponibles pour la variété Horoz. Ainsi la différence entre les proportion des espèces initiallement présentes ne sera pas un facteur pouvant affecter les prédictions que nous réaliserons.


<br>

## Modélisation

La seconde phase de notre étude a consité à mettre en place des modèles afin de classer correctement les grains selon leur variété. 

### Séparation du jeu de données et standardisation

Pour cela, nous avons du séparer notre jeu de données : en premier lieu en les X (variables explicatives) et le y (variable d'intérêt recodée en 0 pour Dermason et 1 pour Horoz), mais également entre le jeu d'entraînement (80%) et le jeu de test (20%). Une fois cette séparation effectuée, nous avons standardiser nos X_train et X_test afin de mettre sur une même échelle nos différentes variables explicatives et ce de façon indépendente entre les jeux train et test.

### Les modèles et les métriques

Nous avons choisi d'appliquer 7 modèles en conservant dans un premier temps les paramètres d'origine proposés. Après avoir entrainé nos modèles sur le jeu test, nous l'avons tester avec notre jeu test. Cela nous a donné les résultats suivants :

<div align="center">

| Modèles| Matrice de confusion | Accuracy | F1 Score
|--|:--:|:--:|:--:|
|Linear SVC| <table><tr><td>400</td><td>0</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|SDG Classifier| <table><tr><td>400</td><td>0</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|SVM linear| <table><tr><td>400</td><td>0</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|SVM rbf| <table><tr><td>399</td><td>1</td></tr><tr><td>5</td><td>367</td></tr></table> | 0.99 | 0.99 |
|SVM poly| <table><tr><td>400</td><td>0</td></tr><tr><td>8</td><td>364</td></tr></table> | 0.99 | 0.99 |
|Logistic Regression| <table><tr><td>400</td><td>0</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|Random Forest| <table><tr><td>400</td><td>0</td></tr><tr><td>5</td><td>367</td></tr></table> | 0.99 | 0.99 |

<i>Légende </i>
<br>
</div>

La matrice de confusion des différents modèles nous permet de nous rendre compte des grains correctement associés à leur variété ainsi que des grains dont la prédiction a été d'une variété à laquelle ils n'appartiennent pas. Grâce à ces matrices, nous obtenons 2 métriques permettant d'évaluer la pertinence de nos modèle : l'accuracy et le F1 score.

On constate que l'ensemble des modèles apportent des prédictions proches de la réalité dans la classification des grains de haricots secs avec des accuracy et F1 score de 0,99 pour chacun des modèles testés. En observant plus précisément les matrices de confusion, on se rend compte qu'il y a davantage de grains dont la prédiction est d'appartenir à la variété Dermason alors qu'ils viennent de la variété Horoz que l'inverse. 

Avec uniquement ces informations, il n'est pas facile de choisir un modèle plus pertinent que les autres.

### La cross validation des modèles d'origine

Afin d'évaluer la qualité des modèles précédemment élaborés, nous avons également eu recours à de la cross validation en choisissant un nombre de K-folds de 5 et en nous intéressant aux accuracy moyennes.

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/7.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

<div align="center">

| Modèles            | Accuracy moyenne |
|--------------------|:--------:|
| Linear SVC         | 0.9912   |
| SDG Classifier     | 0.9903   |
| SVM linear         | 0.9919   |
| SVM rbf            | 0.9929   |
| SVM poly            | 0.9893   |
| Logistic Regression| 0.9906   |
| Random Forest      | 0.9919   |

<i>Légende </i>
<br>
</div>

Comme nous pouvions nous y attendre, les accuracy moyennes sont proches au sein des différents modèles. Toutefois celui ayant la plus forte est le SVM rbf avec une accuracy moyenne de 0.9929. C'est donc ce modèle qui semble être le plus pertinent.


### Optimisation des modèles

Dans un deuxième temps, nous avons relancé nos modèles mais cette fois-ci en ayant modifié leurs paramètres afin de tenter de les optimiser. Pour cela nous avons utilisé GridSearch et RandomizedSearch. Les résultats obtenus sur le jeu test après la phase d'entrainement sur le jeu train sont les suivants.

<div align="center">

| Modèles| Matrice de confusion | Accuracy | F1 Score
|--|:--:|:--:|:--:|
|Linear SVC| <table><tr><td>400</td><td>0</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|SDG Classifier| <table><tr><td>399</td><td>1</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|SVM rbf| <table><tr><td>400</td><td>0</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|Logistic Regression| <table><tr><td>400</td><td>0</td></tr><tr><td>6</td><td>366</td></tr></table> | 0.99 | 0.99 |
|Random Forest| <table><tr><td>400</td><td>0</td></tr><tr><td>5</td><td>367</td></tr></table> | 0.99 | 0.99 |

<i>Légende </i>
<br>
</div>

Nous constatons peu de changements dans ces nouveaux modèles en comparaison aux originaux. En effet les accuracy et F1 score restent de 0.99 et seulement quelques changements mineurs sont observés dans les matrices de confusion.

### La cross validation des nouveaux modèles

Cette fois-ci également, nous avons effectué une cross validation avec 5 folds à partir des modèles obtenus.

<br>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/8.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<br>

<div align="center">

| Modèles            | Accuracy moyenne |
|--------------------|:--------:|
| Linear SVC         | 0.9918   |
| SDG Classifier     | 0.9906   |
| SVM rbf            | 0.9919   |
| Logistic Regression| 0.9909   |
| Random Forest      | 0.9922   |

<i>Légende </i>
<br>
</div>

Avec une accuracy moyenne de 0.9922, le modèle Random Forest est celui le plus pertinent parmi les 5.


### Le meilleur modèle

Au vu des résultats obtenus, si nous ne devons retenir qu'un modèle se sera celui SVM avec un kernel rbf de départ. Ses paramètres sont les suivants : 

{'C': 1.0,
 'break_ties': False,
 'cache_size': 200,
 'class_weight': None,
 'coef0': 0.0,
 'decision_function_shape': 'ovr',
 'degree': 3,
 'gamma': 'scale',
 'kernel': 'rbf',
 'max_iter': -1,
 'probability': False,
 'random_state': 42,
 'shrinking': True,
 'tol': 0.001,
 'verbose': False}

## Interprétabilité du meilleur modèle


<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/9.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/10.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/11.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/12.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/13.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>

<div align="center">
  <img 
  src="https://github.com/mariekrh/SVM/blob/main/Projet/Images/14.png"
  width="600" />
  <br>
  <i>Légende </i>
  <br><br>
</div>


## Conclusion


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

<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Projet M2 ECAP – Classification des haricots secs</title>
</head>
<body>
  <h1 align="center">M2 ECAP – Machine Learning<br>Classification des haricots secs</h1>
  <h3 align="center">Cassandre Orhan & Marie Kerhoas – Mai 2025</h3>
  <hr>

  <h2>1. Introduction</h2>
  <p>
    Ce projet a pour objectif d'étudier un jeu de données morphologiques de haricots secs afin de construire un modèle de machine learning capable de prédire leur variété (Seker, Barbunya, Bombay, Cali, Dermosan, Horoz et Sira).
    Pour cela, nous avons mené une analyse complète, allant de l'exploration des données à la modélisation supervisée, en privilégiant notamment les SVM (Support Vector Machines).
  </p>

  <h2>2. Présentation des données</h2>
  <p>
    Le jeu de données contient des caractéristiques morphologiques extraites d’images de haricots. Parmi elles :
  </p>
  <ul>
    <li><b>Area, Perimeter :</b> Mesures de surface et de contour</li>
    <li><b>Major/Minor axis length :</b> Dimensions principales</li>
    <li><b>Aspect ratio, Eccentricity :</b> Formes géométriques</li>
    <li><b>Roundness, Solidity, Compactness :</b> Indices de circularité</li>
    <li><b>14 ShapeFactors :</b> Combinaisons mathématiques de formes</li>
    <li><b>Class :</b> La variable cible représentant la variété du haricot</li>
  </ul>

  <h2>3. Nettoyage et préparation</h2>
  <p>
    Aucun traitement de données manquantes n’a été nécessaire. Nous avons cependant :
  </p>
  <ul>
    <li>Standardisé les variables numériques avec <code>StandardScaler</code></li>
    <li>Appliqué un <b>winsorizing</b> pour réduire l’effet des valeurs extrêmes</li>
    <li>Converti la cible en labels numériques pour les modèles de classification</li>
  </ul>

  <h2>4. Analyse exploratoire</h2>
  <p>
    Une exploration visuelle avec <code>seaborn</code> et <code>plotly</code> a permis de :
  </p>
  <ul>
    <li>Observer la distribution des variables par classe</li>
    <li>Détecter d’éventuelles redondances (forte corrélation entre certaines mesures comme Area et Convex Area)</li>
  </ul>

  <h2>5. Modélisation</h2>
  <p>
    Plusieurs modèles de classification ont été testés :
  </p>
  <ul>
    <li><b>Régression logistique</b></li>
    <li><b>SVM linéaire et SVM à noyau RBF</b></li>
  </ul>
  <p>
    Après recherche d’hyperparamètres via <code>GridSearchCV</code>, les meilleurs résultats ont été obtenus avec <b>le modèle SVM à noyau RBF</b>.
  </p>

  <h2>6. Évaluation</h2>
  <p>
    Les performances des modèles ont été comparées à l’aide des métriques suivantes :
  </p>
  <ul>
    <li>Accuracy</li>
    <li>F1-score</li>
    <li>Recall / Precision</li>
    <li>Matrice de confusion</li>
  </ul>
  <p>
    Le modèle final atteint une accuracy supérieure à 90%, avec une bonne généralisation sur l’ensemble test.
  </p>

  <h2>7. Interprétabilité</h2>
  <p>
    Pour comprendre les décisions du modèle, nous avons utilisé :
  </p>
  <ul>
    <li><b>Permutation Feature Importance :</b> importance globale des variables</li>
    <li><b>SHAP :</b> contributions locales de chaque variable sur des prédictions individuelles</li>
  </ul>

  <h2>8. Conclusion</h2>
  <p>
    Ce projet a permis de démontrer l’efficacité des modèles d’apprentissage supervisé sur un problème de classification multi-classes à partir de données morphologiques simples.
    Le modèle SVM s’est montré performant, et les outils d’interprétabilité nous ont offert une meilleure compréhension du processus de décision.
  </p>

  <hr>
  <p><i>Ce document accompagne le notebook Python principal, contenant les codes, visualisations et résultats détaillés.</i></p>
</body>
</html>


Bibliothèque image 
![image sur Github](https://github.com/user-attachments/assets/b83a530b-67f1-4d2c-8abd-0315de730387)






