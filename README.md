> Showcase repository: the code and data of this project are private; this README describes it. / Dépôt vitrine : le code et les données de ce projet sont privés ; ce README le décrit.

# QuestFleet

An Android agent installed on each Meta Quest headset and a web dashboard to run a fleet of headsets in a room.

## The problem

At an engineering school, a virtual reality room holds dozens of headsets. Meta's console (Horizon Managed Services, HMS) manages accounts and installs applications, but it cannot send a message to a headset, show what it displays, or keep it from going to sleep. QuestFleet complements HMS without replacing it. It is meant for the teacher or facilitator running a session.

## How it works

- HMS installs the QuestFleet agent on each headset, in critical mode.
- The agent connects to the server over MQTT on secure WebSocket (port 443) and reports its state: battery, Wi-Fi, current application, version.
- The server keeps presence and the history of commands (success, error, timeout).
- The dashboard sends commands to one headset or to a selection: message, application launch, volume, wake-up, casting.
- Casting uses WebRTC, with a TURN relay when the direct connection fails.
- A connector reads the HMS console to pick up each headset's name and group.

## What is built

In service. Agent at version 1.0.44.

- Messages shown in the Meta home screen and on top of a VR application that keeps running; shared pre-written messages.
- Casting of a headset's screen and sound, player microphone, casting wall shareable through a revocable link.
- Voice message to one or all headsets.
- Remote application launch.
- Ring a headset to find it.
- "Always awake" mode with automatic screen wake-up.
- "Worn / set down" detection from the headset's gyroscope.
- Controller vibration, only while the headset is worn.
- Remote agent update, silent when the agent is its own installer, otherwise through HMS.
- Import of the names and groups of 38 headsets from HMS.

Observed limit: a headset in deep sleep or switched off cannot be woken remotely. No fleet management console can do it.

## What is public

This page is public; the dashboard requires an account and the code stays private.

## Tech stack

- Android agent in Java, native OpenXR activity for the controllers
- FastAPI server, SQLite database, JWT authentication
- Mosquitto (MQTT over WebSocket)
- WebRTC and coturn
- Docker, Traefik
- GridStack for the dashboard grid
- Playwright for the HMS connector

---

## Version française

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
