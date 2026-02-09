Détection de Fraudes Bancaires par Autoencodeur
Ce projet vise à détecter automatiquement les transactions frauduleuses dans un ensemble de données bancaires en utilisant un autoencodeur, un type de réseau de neurones.
Problème
Les fraudes bancaires représentent moins de 1% des transactions, ce qui rend leur détection difficile avec les méthodes classiques. L’objectif est de développer un modèle capable d’identifier ces transactions anormales.
Données
Le jeu de données contient 1 000 000 de transactions bancaires avec les variables suivantes :
distance_from_home : distance entre le lieu de transaction et le domicile
distance_from_last_transaction : distance depuis la dernière transaction
ratio_to_median_purchase_price : ratio par rapport au prix d’achat médian
repeat_retailer : achat chez un commerçant déjà visité (0 ou 1)
used_chip : utilisation de la puce (0 ou 1)
used_pin_number : utilisation du code PIN (0 ou 1)
online_order : commande en ligne (0 ou 1)
fraud : variable cible (0 = légitime, 1 = fraude)
Méthode
Nous avons utilisé un autoencodeur, un réseau de neurones qui apprend à reconstruire les données normales. Lorsqu’une transaction frauduleuse est présentée, l’erreur de reconstruction est élevée, ce qui permet de la détecter comme anomalie.
Les étapes réalisées sont :
-	Chargement et exploration des données
-	Normalisation des variables numériques avec StandardScaler
-	Entraînement de l’autoencodeur uniquement sur les transactions légitimes
-	Calcul de l’erreur de reconstruction sur l’ensemble des données
-	Définition d’un seuil pour identifier les anomalies
Architecture du modèle
L’autoencodeur est composé de :
Encodeur : 7 entrées, puis couches de 64, 32, 16 et 8 neurones
Décodeur : couches de 8, 16, 32, 64 neurones, puis 7 sorties
Fonction d’activation : ReLU
Couche latente : 8 neurones
Cette architecture compresse progressivement l’information pour apprendre une représentation compacte des transactions normales.
Hyperparamètres
Après plusieurs tests, les hyperparamètres retenus sont :
Taux d’apprentissage : 0.001
Taille de batch : 128
Nombre d’époques : 20
Dimension latente : 8 neurones
Optimiseur : Adam
Fonction de perte : Mean Squared Error (MSE)
Résultats
Le modèle détecte efficacement les fraudes. Les principaux facteurs de fraude identifiés sont :
used_chip = 0 : les transactions sans puce présentent un risque élevé
online_order = 1 : les achats en ligne sont plus souvent frauduleux
distance_from_home élevée : les transactions loin du domicile sont suspectes
Exemples d’anomalies détectées :
Transaction 799776 : achat en ligne avec distance élevée du domicile
Transaction 472444 : transaction sans puce et sans code PIN
Transaction 44453 : montant anormalement élevé par rapport à la médiane
Transaction 150332 : nouveau commerçant avec distance élevée depuis la dernière transaction
Transaction 982211 : paiement sans puce combiné à un achat en ligne
Technologies utilisées
Python 3
PyTorch
Pandas
NumPy
Scikit-learn
Matplotlib
Installation et exécution
Cloner le dépôt : https://github.com/wassimdiallo67-alt/D-tection-de-fraude-bancaire-
Installer les dépendances : pip install torch pandas numpy scikit-learn matplotlib
Placer le fichier credit_card_data.csv dans le même dossier que le notebook
Exécuter le notebook Jupyter
Conclusion
L’autoencodeur est une approche efficace pour détecter les anomalies dans des données déséquilibrées. Les transactions sans puce, les achats en ligne et les distances élevées sont les principaux indicateurs de fraude identifiés par le modèle.
Auteur
Wassim Diallo
Étudiant en Informatique - Intelligence Artificielle
La Cité collégiale, Ottawa
wassimdiallo67@gmail.com

