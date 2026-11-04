[English](README.md) · **Français**

> Dépôt vitrine : le code et les données de ce projet sont privés ; ce README le décrit.

# QuestFleet

Un agent Android installé sur chaque casque Meta Quest et un tableau de bord web pour piloter une flotte de casques en salle.

## Le problème

Dans une école d'ingénieurs, une salle de réalité virtuelle compte des dizaines de casques. La console de Meta (Horizon Managed Services, HMS) gère les comptes et installe les applications, mais elle ne permet pas d'envoyer un message à un casque, de voir ce qu'il affiche ou de l'empêcher de se mettre en veille. QuestFleet complète HMS sans le remplacer. Il sert à l'enseignant ou à l'animateur qui conduit une séance.

## Comment ça marche

- HMS installe l'agent QuestFleet sur chaque casque, en mode critique.
- L'agent se connecte au serveur en MQTT sur WebSocket sécurisé (port 443) et remonte son état : batterie, Wi-Fi, application en cours, version.
- Le serveur garde la présence et l'historique des commandes (réussite, erreur, délai dépassé).
- Le tableau de bord envoie des commandes à un casque ou à une sélection : message, lancement d'application, volume, réveil, casting.
- Le casting passe par WebRTC, avec un relais TURN quand la connexion directe échoue.
- Un connecteur lit la console HMS pour reprendre le nom et le groupe de chaque casque.

## Ce qui est construit

En service. Agent en version 1.0.44.

- Messages affichés dans l'accueil Meta et au-dessus d'une application VR qui continue de tourner ; messages pré-écrits partagés.
- Casting de l'écran et du son d'un casque, micro du joueur, mur de casting partageable par lien révocable.
- Message vocal vers un ou tous les casques.
- Lancement d'application à distance.
- Faire sonner un casque pour le retrouver.
- Mode « toujours éveillé » avec rallumage automatique de l'écran.
- Détection « porté / posé » à partir du gyroscope du casque.
- Vibration des manettes, casque porté seulement.
- Mise à jour de l'agent à distance, silencieuse quand l'agent est son propre installateur, sinon par HMS.
- Import des noms et groupes de 38 casques depuis HMS.

Limite constatée : un casque en veille profonde ou éteint ne peut pas être rallumé à distance. Aucune console de gestion de flotte ne le permet.

## Ce qui est public

Cette vitrine est publique ; le tableau de bord demande un compte et le code reste privé.

## Pile technique

- Agent Android en Java, activité native OpenXR pour les manettes
- Serveur FastAPI, base SQLite, authentification JWT
- Mosquitto (MQTT sur WebSocket)
- WebRTC et coturn
- Docker, Traefik
- GridStack pour la grille du tableau de bord
- Playwright pour le connecteur HMS
