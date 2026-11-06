**English** · [Français](README.fr.md)

**Anthony Hunt** · [Project page on ingevision.cloud](https://ingevision.cloud/?lang=en&p=questfleet) · [LinkedIn](https://www.linkedin.com/in/anthony-hunt-3948a9196) · [GitHub profile](https://github.com/anthohunt)

> Showcase repository: the code and data of this project are private; this README describes it.

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
