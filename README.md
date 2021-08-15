# Correlation & Anova
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Correlation%20%26%20Anova.py

Lorsque l'on effectue une analyse ux analytics et que l'on souhaite savoir si des variables ont lien l'une les une avec les autres, plusieurs tests statistique peuveut permettre d'analyser cette question. Le test de correlation est un test statistique qui permert de savoir de quel est le degré relation linéaire entre 2 variables numériques. Il calcule un coefficient de correlation pouvant aller de -1 à 1. Plus ce coefficient est proche de 1 en valeure absolue plus il a une forte relation de proportionnalité (positif ou négatif) entre ces 2 variables et donc que ces variables sont liées entre elles. Plus ce coefficient est proche de 0 moins ces variables sont liées entre elles.

Également dans le cadre d'un A/B testing on peut être amener à comparer le nombre moyens de conversions sur plusieurs effectifs mais il ne serait pas pertinent de comparer des moyennes entre un effectif de 10 individus et un autre de 10 000. Le test statisque anova nous permet justement savoir si les effectifs sont suffisament importants pour conclure de la significativité des résultats. En statistique on pose l'hypothèse nulle (H0) estimant d'une egalité entre les groupes. Si cette hypothèse est vraie alors la différence de moyenne est du à un echantillon trop faible puisque chaque effectif vienne de la même distribution. En augmentant la taille de l'echantillon les moyennes devraient tendre vers une même valeure. En revanche si l'hypothese nulle est fausse alors même en augmentant la taille de l´echantillon on ne pourrait pas faire disparaitre les diffences entre les moyennes puisque les effectifs viendraient de 2 distributions distinctes. Le test calcule la probabilité (p-valeure) d'observer ces resultats sous H0 et si celle-ci est très petite (souvent inférieure au seuil de 0,05) alors on rejette H0. On se tourne alors vers l'hypothèse alternative (H1), que nos effectifs proviennent de 2 distributions significativement différentes et on conclut alors à une différence significative entre les moyennes. En revanche si la p-valeure est supérieure à 5% alors on ne peut pas rejeter H0.

# Chi-2 & Logistic Regression 
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Chi-2%20%26%20Logistic%20Regression.py

En ux analytics, lorsqu'on souhaite par exemple savoir si la mis à jour d'une page a un effet significatif sur les conversions, on peut utilser le test statistique du chi-2 dans un process d'A/B testing afin d'analyser la significativité des résultats. Le test du chi-2 est un test statique qui comme le test de correlation permert de savoir si des variables sont liées entre elles mais cette fois 2 variables catégorielles. Ici la premiere variable sera le type de page vue (orginale, A ou B) et la seconde, le fait d'effectuer une conversion (oui ou non). Comme tout test statistique, le test du chi-2 pose H0 estimant d'une egalité entre les groupes, c'est à dire ici qu'il y aurait en propotion autant de conversions effectuées parmis les personnes qui ont vu la page originale que parmis celles qui ont vu la page A et celles qui ont vu la page B, et l'hypothèse alternative H1 estimant d'une difference entre les groupes. Si la p-valeure calculé par le test est inférieure à 5% alors on rejette H0 et on se tourne vers H1 pour en conclure qu'il y a bien un lien significatif entre le type de page vue et le fait d'effectuer une conversion. 

Si à la suite du test du chi-2 on conclut à un lien significatif entre les 2 varibles et que la variable dépendante est   dichotomique (2 modalités) alors il est pertinent d'effectuer un modèle de regression logistique binomiale afin de mesurer l'impact de la variable explicative sur celle-ci. Ici on modélise le fait d'effectuer une conversion (variable dépendante) en fonction du type de page vue (variable explicative). Le modèle de regression logistique calcule la probabilité qu'un individu à de prendre la premiere modailité pour la variable dépendante sachant ses modalités pour les variables explicatives par rapport au profil de réference. Généralement on prend comme profil de réference les modalités des variables exlicatives qui ont le plus fort effectif mais ici dans le cadre d'un A/B testing le profil de réference sera le fait d'avoir vu la page orginale. On poura ainsi mesurer de combien fait évoluer les chances d'effectuer une transaction le fait d'avoir vu la page A ou B par rapport au fait d'avoir vu la page originale.

Également si on veut maintenant modéliser une variable numérique en fonction de variables catégorielles on peut utiliser le modele lineaire généralisé qui comme la regression logistique calcule l'impact des autres modalités des variables explicatives sur la variable dépendante par rapport au profil de reférence. On peut par exemple pour un site e-commerce analyser le montant des transactions en fonction des versions du site et voir de combien fait evoluer ce motant le fait d'avoir vu la page A ou B par raport au fait d'avoir vu la page originale.


# K-Means Clustering
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Clustering%20K-Means.py

En markerketing digital il est assez important de bien connaitre ses consomateurs, la facon dont ils se comportent afin de bien les segmenter et ainsi pouvoir diriger des actions ciblées. Le modèle de machine learning de clustering k-means peut justement aider à effectuer une segmentation optimale car il permet de découper une population de manière ce que les groupes constitués soient à la fois en intra les plus homogènes possible et et en extra les plus differents les un des autres. Dans un contexte e-commerce on peut par exemple segmenter les transactions afin de mieux comprendre le compotertement des acheteurs sur le site. On va donc crées un jeu de données provennant des données Google Analytics requêtées dans BigQuery indicant pour chaque achat le device et son os, la source de traffic et de campagne de l'acheteur, son pays, les produits et catégories produits achetés, le nombre de visites que l'acheteur a effectué sur les produits et catégories produits achetés, et enfin le CA.

L'inconvenient du modele K-Means est qu'on ne sait pas a priori quel est le nombre optimal de groupes (clusters) il faut choisir pour que le population soit separer de maniere à ce que les clusters constitués soient à la fois le plus homogenes possible et differents les un des autres. On utlise pour cela la courbe d'elbow en testant une décomposition de 1 à 10 groupes.

![Courbe d'elbow](https://user-images.githubusercontent.com/83826055/129334001-457b71dd-c30f-43de-897e-d2dab6f01a60.png)

Le nombre optimal de clusters qu'il faut choisir afin que la population soit découpée de la meilleure des manières est celui du point des abscisses où la courbe marque une cassure et devient linéaire. On voit ici que la meilleure des manieres de segmenter nos acheteurs est de les séparer en 3 groupes. On voit que ce qui caracterise le plus ces segments sont le niveau de CA. On renvoie ainsi ces résultats vers Google Cloud pour une analyse plus en détail de ce qui différencie les clusters constitués sur outils BI : https://datastudio.google.com/s/hRcohz4T4DI

# Kaplan Meier Survival
Demo : https://github.com/MarvinEdorh/Data-Mining/blob/main/Kaplan%20Meier%20Survival.py

Lorsqu'on effectue un A/B testing on peut également être amenner à analyser la performance du site en terme de durée. Quelle version permert d'effectuer une conversion le plus rapidement ? Pour cela il nécéssaire d'effectuer une analyse de servie de Kaplan Meier. Souvent utilisée en medecine et en finance cette analyse permet de calculer la probabilité qu'un evenement à de ne pas se produire (le décès) à  un instant t. C'est la raison pour laquelle elle se nomme l'analyse de survie, la fonction S(t) donne la probabilité d'etre en vie à l'instant t. Pendant l'analyse on oberve des individus pour qui après une durée t soit l'evenement est intervenu (ils sont décédés) soit on a arreté de les obeserver (ils sont cencurés).

Dans un contexte ux on peut symboliser le decès par le fait d'effectuer une conversion, sur un site e-commerce on va par exemple générer un jeu de données provennant des données Google Analytics requêtées dans BigQuery indicant pour chaque visiteur la durée entre sa premiere visite et son premier achat (le décès) s'il en a effectué, et la durée entre sa premiere et sa derniere visite s'il n'en a pas effectué (la censure). On indique également le device sur lequel il a effectuer la transaction ou sa dernière visite sinon afin de voir quelle version du site est la plus performante.

![KMF](https://user-images.githubusercontent.com/83826055/129444429-fcef0f33-b30f-4c5c-9b22-af75347ed59e.png)

On voit ici la survie globale du site indépendament des versions qui signifie ici la probabilité de n'avoir effectuer aucun achat x jours après sa première viste (0% après 1 jour, 60% apres 1 ans). Mais l'interet de l'analyse est bien de segmenter les individus afin de voir dans quelle situation la survie est la meilleure ou la moins bonne suillant le contexte de l'analyse.

![KMF_Device](https://user-images.githubusercontent.com/83826055/129444431-0271e2aa-c5cc-4988-9497-2b6b61337bb1.png)

On regarde maintenant la survie en fonction du device et on constate que la survie la moins bonne est celle de la version du site sur desktop, ce qui signifie que l'on y décède plus rapidement. Dans un contexte de santé cela sera négatif mais ici dans notre contexte e-commerce cela signifie en fait que la version du site sur desktop est la plus performante en terme de durée pour géner des conversions. La probailité de n'avoir effectuer aucun achat 200 jours après sa première visite est de 95% sur mobile et tablet et seulement de 75% sur desktop. Afin de savoir si ces résultats sont significatif on effectue le test statistique du log rank qui pose H0 et H1, et conclue à une significativité si la p-valeure calculée sous H0 est inferieure à 5%

![KMF_2](https://user-images.githubusercontent.com/83826055/129450587-cf45114a-ea53-49d4-b7ee-a1bb04a8b7f3.png)

Egalement s'il on souhaite maintenant non plus analyser la rapidité des conversions ma la durée de retention, on selection plus la durée avec le premier mais le dernier. On maintenant que la survie en terme de retention est moins bonne, on voit ici que la probabilité qu'un individu continue d'acheter sur le site un ans après sa première visite est de 50%

![KMF_Device_2](https://user-images.githubusercontent.com/83826055/129450589-e52c90a2-8391-4d86-9827-43318689c2ae.png)

Si on analyse maintenant la survie en fonction du device, on voit que c'est la version sur mobile qui a la meilleure retention. La probabilité qu'un individu continue d'acheté un ans après sa premiere visite est de 95% sur mobile et de 40% sur desktop. Ce resultat peut néanmoins comporter un biais car on voit que nos fonctions de conversions de retentions sont assez similaires, cela peut signifier en fait que la plus part des invidus n'ont en en fait realisé que un seul achat et que ceux qu'il l'ont fait sur mobile l'ont fait tardivement.
