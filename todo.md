Projet Java : Football Manager
Ce projet consiste en la création d'une application Java pour gérer des statistiques et des matchs de football. Ce projet couvre l'utilisation de plusieurs concepts Java comme les collections, les exceptions, les threads, et te permettra d'appliquer les connaissances que tu as révisées.
Objectif du projet
L'application gère des joueurs, des équipes, enregistre les résultats des matchs et analyse les performances des joueurs par compétition (ex. Premier League, Ligue des Champions).
________________________________________
Étape 1 : Définir les classes de base
Classe Player
Représente un joueur de football.
•	Attributs : nom, âge, poste (attaquant, défenseur...), équipe, nombre de buts, nombre de passes.
•	Collections : Utilise un Set pour enregistrer les joueurs et éviter les doublons.
•	Méthodes :
o	addGoal() et addAssist() pour augmenter les statistiques du joueur.
o	Surcharge les méthodes equals et hashCode pour éviter les doublons dans le Set.
Classe Team
Représente une équipe de football.
•	Attributs : nom de l’équipe, ligue, pays.
•	Collections : Utilise un Set pour contenir les objets Player.
•	Méthodes :
o	addPlayer(Player player) : Ajoute un joueur à l’équipe, vérifie qu'il n'est pas déjà dans l'équipe.
o	displayPlayers() : Affiche les informations des joueurs de l'équipe (utilise un Iterator pour parcourir le Set).
________________________________________
Étape 2 : Créer une structure de championnat et de compétition
Classe Match
Représente un match de football.
•	Attributs : équipe à domicile, équipe visiteuse, score (sous forme de Map<Team, Integer>), compétition (ex : Premier League, Ligue des Champions).
•	Collections : Utilise un SortedSet pour stocker les matchs triés par date ou par compétition.
•	Méthodes :
o	addGoal(Player player) : Mise à jour du score et des statistiques du joueur.
Classe League
Représente une compétition avec une liste de matchs.
•	Attributs : nom de la compétition, saison (ex. 2023/2024), équipes.
•	Collections : Utilise un NavigableSet<Match> pour stocker les matchs et permettre la navigation.
•	Méthodes :
o	scheduleMatch(Match match) : Ajoute un match au NavigableSet et gère les exceptions en cas de doublon.
o	displayMatches() : Affiche les informations de tous les matchs programmés (utilise un Iterator).
o	nextMatch(Match match) et previousMatch(Match match) : Utilise NavigableSet pour retrouver le match suivant ou précédent dans le calendrier.
________________________________________
Étape 3 : Gestion des statistiques et affichage
Classe StatisticsManager
Gère les statistiques générales des joueurs et équipes.
•	Attributs : aucun en particulier, mais utilise des méthodes statiques.
•	Méthodes :
o	topScorers(List<Player> players) : Retourne une ArrayList triée des meilleurs buteurs (utilise ListIterator).
o	topAssistProviders(List<Player> players) : Retourne une ArrayList triée des meilleurs passeurs.
Classe ExceptionManager
Gère les exceptions personnalisées.
•	Classes d'exceptions :
o	PlayerAlreadyExistsException : Hérite de RuntimeException, déclenchée si un joueur est ajouté deux fois dans une équipe.
o	MatchAlreadyScheduledException : Hérite de RuntimeException, déclenchée si un match est déjà programmé.
•	Blocs try-catch : Dans les méthodes addPlayer() de Team et scheduleMatch() de League pour gérer ces exceptions.
________________________________________
Étape 4 : Tests et application principale
Classe principale : FootballManagerApp
1.	Crée des objets pour Liverpool, d'autres équipes, et des joueurs célèbres.
2.	Planifie des matchs et met à jour les scores.
3.	Affiche les classements des buteurs et passeurs.
Tests spécifiques
•	Tester les doublons de joueur dans Team pour déclencher PlayerAlreadyExistsException.
•	Programmer un match déjà planifié dans League pour tester MatchAlreadyScheduledException.
•	Assertions pour vérifier le bon fonctionnement des Set.
________________________________________
Étape 5 : Planification des matchs avec des Threads
Classe MatchScheduler
Chaque instance de cette classe représente un match programmé dans un thread séparé. Elle permet de simuler le déroulement asynchrone des matchs.
•	Attributs : Match (le match à planifier), délai avant l’exécution.
•	Méthodes :
o	run() : Simule la durée d’un match avec Thread.sleep(), puis met à jour le score des équipes.
Classe League - Gérer la planification des matchs
•	Collections : Ajoute une List<Thread> pour stocker les threads en cours.
•	Méthodes :
o	scheduleAllMatches() : Lance chaque match dans un thread séparé en utilisant MatchScheduler.
o	cancelAllMatches() : Annule tous les matchs programmés si besoin (interrompt chaque thread).
•	Classe principale FootballManagerApp - Attendre les résultats
Structure des Packages
1.	models : Player, Team, Match.
2.	services : StatisticsManager, ExceptionManager.
3.	exceptions : PlayerAlreadyExistsException, MatchAlreadyScheduledException.

