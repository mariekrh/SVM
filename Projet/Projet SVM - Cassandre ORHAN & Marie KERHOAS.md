<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
</head>
<body>
  <h1 align="center">M2 ECAP – Machine Learning<br>Classification des haricots secs</h1>
  <h3 align="center">Cassandre Orhan & Marie Kerhoas – Mai 2025</h3>
  <hr>

  <h2>1. Introduction</h2>
  <p>
    Ce projet a pour objectif d'étudier un jeu de données morphologiques de haricots secs afin de construire un modèle de machine learning capable de prédire leur variété (Seker, Barbunya, Bombay, Cali, Dermosan, Horoz et Sira).
    Pour cela, nous avons mené une analyse complète, allant de l'exploration des données à la modélisation supervisée.
  </p>

  <h2>2. Présentation des données</h2>
  <p>
    Le jeu de données contient des caractéristiques morphologiques extraites d’images de haricots. Parmi elles :
  </p>
  <ul>
  <li><b>Area :</b> Surface d’un haricot, en nombre de pixels</li>
  <li><b>Perimeter :</b> Longueur de la bordure (contour) du haricot</li>
  <li><b>Major axis length :</b> Longueur maximale mesurée sur le haricot</li>
  <li><b>Minor axis length :</b> Longueur perpendiculaire à l’axe principal</li>
  <li><b>Aspect ratio :</b> Rapport entre les axes majeur et mineur</li>
  <li><b>Eccentricity :</b> Excentricité de l’ellipse équivalente</li>
  <li><b>Convex area :</b> Surface du plus petit polygone convexe entourant le haricot</li>
  <li><b>Equivalent diameter :</b> Diamètre du cercle ayant la même surface que le haricot</li>
  <li><b>Extent :</b> Rapport entre la boîte englobante et la surface réelle</li>
  <li><b>Solidity :</b> Rapport entre la surface convexe et la surface réelle</li>
  <li><b>Roundness :</b> Indice de circularité basé sur la formule (4πA)/(P²)</li>
  <li><b>Compactness :</b> Rapport entre le diamètre équivalent et la longueur de l’axe principal</li>
  <li><b>ShapeFactor1 :</b> Premier indicateur de forme</li>
  <li><b>ShapeFactor2 :</b> Deuxième indicateur de forme</li>
  <li><b>ShapeFactor3 :</b> Troisième indicateur de forme</li>
  <li><b>ShapeFactor4 :</b> Quatrième indicateur de forme</li>
  <li><b>Class :</b> Étiquette de classe du haricot (Seker, Barbunya, etc.)</li>
</ul>

  <h2>3. Nettoyage et préparation</h2>
  <p>
    Aucun traitement de données manquantes n’a été nécessaire. Nous avons cependant :
  </p>
  <ul>
    <li>Standardisé les variables numériques avec <code>StandardScaler</code></li>
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
    <li><b>SVC linéaire</b></li>
    <li><b>SDG Classifier</b></li>
    <li><b>Régression logistique</b></li>
    <li><b>SVM linéaire, SVM à noyau RBF et à noyau polynomial</b></li>
    <li><b>Random Forest</b></li>
    
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
  </p>
    
  <h2>8. Conclusion</h2>
  <p>
    Ce projet a permis de démontrer l’efficacité des modèles d’apprentissage supervisé sur un problème de classification multi-classes à partir de données morphologiques simples.
    Le modèle SVM s’est montré performant, et les outils d’interprétabilité nous ont offert une meilleure compréhension du processus de décision.
  </p>

  <h2>9. Discussion </h2>
  <p>
  </p>

  Bibliothèque image à insérer au bon endroit 
    ![image sur GitHub](https://github.com/user-attachments/assets/8c600652-d86f-467e-9afa-e066f6021eac)
   ![image sur Github](https://github.com/user-attachments/assets/d69ed21a-e44b-4f1c-9fa1-680ec2631136)
   ![image sur Github](https://github.com/user-attachments/assets/56ee4ead-f014-4ed6-ad39-43f181eb9f1a)
   ![image sur Github](https://github.com/user-attachments/assets/35316831-13de-48b1-a1a8-06216aa06e2d)
   ![image sur Github](https://github.com/user-attachments/assets/02288ec1-1717-4338-9b87-a38f96a9021d)
   ![image sur Github](https://github.com/user-attachments/assets/c58f0158-211c-4105-8e2c-6ecfc3453f30)
   ![image sur Github](https://github.com/user-attachments/assets/88600098-2b60-44f7-9df5-f6c9be8e370d)
   ![image sur Github](https://github.com/user-attachments/assets/64289d40-2799-474a-99d8-30c10c411155)
   ![image sur Github](https://github.com/user-attachments/assets/70d19798-b7bb-415c-9053-a5ac9e358364)

  <hr>
  <p><i>Ce document accompagne le notebook Python principal, contenant les codes, visualisations et résultats détaillés.</i></p>
</body>
</html>
