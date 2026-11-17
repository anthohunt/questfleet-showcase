[English](README.md) · **Français**

# QuestFleet

**Un tableau de bord web et un agent sur chaque Meta Quest permettent à l'enseignant de voir, caster et piloter toute une salle de casques pendant un cours.**

[![Le vrai tableau de bord avec des casques de démo : trois casques en casting, l'un en grand, un message acquitté par chaque casque, puis une application lancée sur la sélection (cliquer pour la vidéo complète)](docs/demo.fr.gif)](https://drive.google.com/file/d/1qm_Ck3pZvEZFgkB2QJicxVAHOvuQ91IG/view)

*Le vrai tableau de bord, piloté avec des casques de démo ; le casting rejoue une session enregistrée dans un casque. [Vidéo complète (0:59)](https://drive.google.com/file/d/1qm_Ck3pZvEZFgkB2QJicxVAHOvuQ91IG/view)*

## Utilisation

- **Flotte.** Chaque casque avec son nom et son groupe dans la console de Meta (HMS) : en ligne ou injoignable, porté ou posé, batterie, version de l'agent, alertes.
- **Casting.** Écran et son d'un ou plusieurs casques, micro du joueur, une vue en grand ; un mur de casting partagé par un lien révocable.
- **Messages.** Texte affiché dans le casque par-dessus l'application VR en cours, messages pré-écrits, parole en direct au micro vers un ou tous les casques ; chaque casque acquitte.
- **Applications et réglages.** Lancer une application sur la sélection, régler le volume, garder les casques éveillés avec rallumage automatique de l'écran, faire sonner un casque pour le retrouver, faire vibrer ses manettes quand il est porté.
- **Mises à jour de l'agent.** HMS installe l'agent ; un casque en retard sur la version publiée se met à jour dès qu'il se signale.

## Architecture

![Architecture : le navigateur de l'enseignant échange commandes et état avec l'API, qui passe par le broker MQTT jusqu'à l'agent de chaque casque ; chaque casque renvoie son état et, pour le casting, son écran et son son, relayés en direct vers le navigateur ; HMS installe l'agent, et une passerelle navigateur en lit noms et groupes](docs/architecture.svg)

<details><summary>Diagramme en français</summary>

![Architecture : le navigateur de l'enseignant échange commandes et état avec l'API, qui passe par le broker MQTT jusqu'à l'agent de chaque casque ; chaque casque renvoie son état et, pour le casting, son écran et son son, relayés en direct vers le navigateur ; HMS installe l'agent, et une passerelle navigateur en lit noms et groupes](docs/architecture.fr.svg)

</details>

## État

- **Utilisé** à IMT Mines Albi de septembre à octobre 2026 : 17 casques avec l'agent, sur 38 gérés dans HMS.
- **Depuis le 6 novembre 2026**, QuestFleet tourne sur le serveur de l'école, joignable seulement depuis son réseau. Les casques et la passerelle HMS n'y sont pas encore reliés (mise à jour de l'agent à venir), et le casting y demande un relais TURN.
- **Limite connue.** Un casque en veille profonde ou éteint ne peut pas être réveillé à distance.
- **Technologies.** OpenXR pour les manettes, MQTT sur WebSocket, aiortc et coturn, Docker, GridStack ; passerelle HMS en Node.js avec Playwright. Interface en français.

---

**Anthony Hunt** · [ingevision.cloud](https://ingevision.cloud/?p=questfleet) · [LinkedIn](https://www.linkedin.com/in/anthony-hunt-3948a9196) · [GitHub](https://github.com/anthohunt)

Le code et les données de la flotte sont privés.
