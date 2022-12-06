# TP02 - Panneau affichage soccer

## 1 - Directives

### 1.1 - Déroulement du TP

- Remise du travail: 11 janvier 2023, 23:59
- Ce travail est réalisé en équipe de 2 personnes et seuls les membres de cette équipe y contribuent
- Toutes les réponses fournies doivent être originales (produites par l’étudiant ou un membre de l’équipe)
- Toute copie de code, de portion de code, d’algorithme ou de texte doit faire mention de sa source
- L’emprunt ou la copie de code ou de portions de code est interdite
- Tout constat de plagiat, tricherie ou fraude sera automatiquement déclaré à la Direction et les sanctions prévues seront appliquées
- Vous devez utiliser votre dépôt Git et Teams pour faire votre travail : si une situation particulière est détectée, vos commits moduleront votre note dans le groupe et peut même aller jusqu'à un zéro en cas de non participation

## 1.2 - À remettre sur la plateforme d'enseignement Léa

- Un document Word contenant les détails du projet
- Votre code source C++ avec la structure de PlatformIO
- Vous devez fournir le lien d'une vidéo de 5 minutes illustrant le circuit, le code et le fonctionnement :
  - La vidéo doit être déposée sur YouTube
  - En lien non listé
  - La vidéo doit être accessible jusqu'à un an après la remise du travail
  - La vidéo doit être en français

En résumé, vous pouvez simplement archiver le contenu de votre dépôt Git qui devrait contenir tous ces éléments au moment de la remise (-5 points nous devons courir après des éléments de la remise).

## 1.3 - Structure de la remise

- Vous devez remplir le fichier ```AUTHORS.md``` (-5 points si mal rempli). Il donne le nom et matricule des équipiers
- Le lien de la vidéo doit être indiqué dans le document word et dans le fichier ```AUTHORS.md``` (-5 points si mal rempli)
- Votre code source doit être dans le répertoire  ```src``` du présent dépôt Git
- Le répertoire source doit suivre la structure d’un projet Platform.io
- Le répertoire ```doc``` doit contenir votre rapport de TP
- La remise finale doit être faite sur la plateforme d'enseignement Léa

## 2 - Description du projet

Pour promouvoir la santé des jeunes, la municipalité de "Sports En Action" prévoit construire un stade de soccer. Un tableau d’affichage sera installé pour suivre le déroulement du match. Ce tableau, situé au fond du terrain, sera composé de deux éléments : un afficheur numérique et un afficheur à cristaux liquides. À cause des distances, l'usage d'un réseau Sans fil est demandé.

Votre tâche générale consiste à mettre en place un programme pour gérer et afficher les résultats lors des matchs de soccer.

Un match est une structure JSON décrite comme ceci :

- Nom des deux équipes
- Points marqués par chaque équipe
- Nombre total de périodes de jeu
- Durée d'une période de jeu
- Numéro de la période en cours
- Temps courant

Ce système comprend :

- Un microcontrôleur EPS32, modèle esp32doit-devkit-v1
- Un afficheur numérique 4 * 7-segments de forme 99:99
- Un afficheur LCD donnant le nom des deux équipes en jeu
- Un site web permettant aux officiels de saisir les données du match :
  - D'initialiser le match (saisie des noms des deux équipes, le nombre de période et la durée de chacune)
  - Ajouter/annuler un but durant le match
  - Démarrer/interrompre/reprendre une période
  - Terminier le match
  - Heure réelle (Voir NTP et ESP32 RTC) de début de chaque période
- Un bouton poussoir permettant de démarrer/interrompre/reprendre une période
- Les deux autres boutons permettant d’ajouter un but à l’équipe invitée ou à l'équipe locale

Les résultats du match sont sauvegardés dans la mémoire flash de votre application au format JSON
Le système doit récupérer l'heure courante à partir d'un serveur NTP.

Pour accéder au site web, votre système doit se servir d’un point d’accès. Le point d’accès doit être configuré avec un nom et un mot de passe. Le nom et le mot de passe doivent être configurables par l’utilisateur.

## 2.1 - Début et contrôle du match 

Au début du match, l’afficheur LCD indique le nom des deux équipes. Le nom de l’équipe invitée sera placée sur la première ligne, le nom de l’équipe locale sur la deuxième ligne.

L’officiel configure et démarre le chronomètre apparaissant sur l’afficheur numérique. Le format est MM:SS. Le chronomètre commence à 00:00 et s’arrête à la fin de la période courante ou lorsque l'officiel arrête le jeu momentanément.

L’officiel démarre la période suivante en appuyant sur le bouton poussoir. Le chronomètre redémarre et le match reprend et ainsi de suite pour toutes les périodes du match.

Le chronomètre est mis à jour à toutes les secondes.

## 2.2 - Déroulement du match 

L’afficheur numérique joue deux rôles. Pendant deux secondes, il affiche le temps de jeu. Pendant deux autres secondes, il affiche le pointage; les deux premiers segments donnent le pointage de l’équipe adverse et les deux derniers segments donnent le pointage de l’équipe locale.

À l’aide de son téléphone cellulaire, l’officiel peut :

- Ajouter/annuler les points comptés par une des deux équipes
- Interrompre/redémarrer le chronomètre
- Afficher les données du match en cours

Vous devez proposer une façon visuelle d’illustrer les temps d’arrêt au tableau d’affichage

## 2.3 - Fin du match

Le match prend fin lorsque l'officiel force la fin du match avec son téléphone cellulaire. Pour éviter de "faux points", le pointage doit être bloqué, durant les pauses et à la fin du match.

Une période de prolongation pourra être autorisée par l'officiel. Cette période est sous le contrôle de l'officiel. 

S'il y a débordement du temps écoulé (> 99:59), une DEL s'allume pour indiquer les centaines! 

Les résultats sont transférés dans la flash dans le format d’un fichier JSON. En cas de panne, les données doivent être préservées.

## 3 - Détail de l'évaluation

### 3.1 - Répartition des points

Vous devez faire le travail en équipe de 2 personnes, au maximum. Le document doit indiquer les tâches respectives que chaque personne aura fait.

1. Préparation du projet : (35%)
   - Contexte du projet (10%)
   - Planification, attribution des tâches (5%)
   - Description des étapes du projet (5%)
   - Diagramme de classes (5%)
   - Schéma électronique du montage (5%)
   - Inventaire des pièces et évaluation du coût (5%)

2. Registre des heures consacrées au projet (5%)
   - Le registre doit indiquer la répartition des tâches. Si le travail est fait en équipe, le registre doit montrer les tâches respectives que chaque personne aura fait avec le nombre d’heures par tâche.

3. Vidéo de 5 minutes illustrant le fonctionnement (10%)
   - Présentation rapide du circuit (3%)
   - Présentation rapide de la structure du code et des choix de conception (4%)
   - Présentation du fonctionnement (3%)

4. Fonctionnalités (50%)
   - Démarrage/reprise entre les périodes/fin du match (5% par bouton, +5%  par le site web)
   - Ajout/annulation d’un but (5% par bouton, +5%  par le site web)
   - Démonstration personnalisée du temps d’arrêt (5%)
   - Redémarrage du match en cours en cas de coupure d'électricité (10%)
   - Récupération de l'heure courante à partir d'un serveur NTP et du RTC d'ESP32 (5%)
   - Affichage alterné du chronomètre et du pointage des équipes (10%)
   - Optionnellement, total des pénalités "cartons jaunes/rouges" de chaque équipe durant le match (+5%)
   - Optionnellement, tout effet visuel permettant de stimuler l'entrain des spectateurs (+5%)

Le respect des bonnes pratiques de programmation modulaire et orientée objet est évalué avec les fonctionnalités.

Durant l'évaluation de vos projets, les enseignants vont consulter l'historique de Teams (Sharepoint) et de Git. La non ou la mauvaise utilisation de ces deux outils entraîne une pénalité de 20% sur la note globale.

Pourquoi ces outils ?

- Outils similaires utilisés pour collaborer en entreprise
- Validation du travail de chaque partenaire

### 3.2 - Critères appliqués durant l'évaluation

L'évaluation du travail est effectuée par les enseignants de l'UE en se basant sur :

- L'historique de Git et de Teams/Sharepoint font office de référence pour évaluer la proportion du travail effectué par chaque équipier

- La qualité et le contenu du code source :

  - Conformité du code et des normes d'écriture utilisées dans le cours
  - Respect des bonnes pratiques (STUPID / SOLID)
  - Fonctionnalité du code
  - Facilité de lecture du code
  - Modularité
  - Modularité et utilisation adéquate de la POO
  - Modèle objet
  - Paramétrisation du code
  - Utilisation de constantes
  - Utilisation de fichiers de configuration
  - Optimisation de la mémoire
  - Bonne utilisation des contraintes matérielles
  - Bonne utilisation des bibliothèques
  - Nommage
  - Propreté et homogénéité du code
  - Initialisations / fuite mémoire
  - etc.

- La qualité et le contenu du document word :
  - Français
  - Schéma électrique et diagramme de classes
  - Clarté et précision des explications
  - Mise en page
  - Page de présentation
  - etc.

- La qualité et le contenu de la présentation vidéo :
  - Vidéo
  - Audio
  - Explication orale des choix de conception (Ex. "Nous avons fait une classe A et une classe B. Voici la méthode M" => 0% "Nous avons fait une classe A afin de pouvoir simplifier la gestion de E et de permettre de le remplacer par F un peu plus tard et limiter les impacts en cas de XYZ" => 100% si pertinent)
  - etc.

Tout partage de code, d'explication, de bouts de texte, etc. est considéré comme du plagiat. Pour plus de détails, consultez le site (et ses vidéos) [Sois intègre du Cégep de Sainte-Foy](http://csfoy.ca/soisintegre) ainsi que [l'article 6.1.12 de la PÉA](https://www.csfoy.ca/fileadmin/documents/notre_cegep/politiques_et_reglements/5.9_PolitiqueEvaluationApprentissages_2019.pdf)
