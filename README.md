# README

[![Release](https://img.shields.io/docker/v/jcpd/dknr-apsystems?sort=semver)](https://img.shields.io/docker/v/jcpd/dknr-apsystems?sort=semver)
[![Pull](https://img.shields.io/docker/pulls/jcpd/dknr-apsystems)](https://img.shields.io/docker/pulls/jcpd/dknr-apsystems)
[![Issue](https://img.shields.io/github/issues/jcdenis/dknr-apsystems)](https://img.shields.io/github/issues/jcdenis/dknr-apsystems)
[![License](https://img.shields.io/github/license/jcdenis/dknr-apsystems)](https://github.com/JcDenis/dknr-apsystems/blob/master/LICENSE)


## A propos

**dknr-apsystems** est un projet consacré à la récupération et à l'exploitation des données des onduleurs APSystems en local. Ce projet n'utilise pas le cloud APSysttems mais attaque directement l'API de l'ECU.

[![Dashboard Screenshot](https://github.com/JcDenis/dknr-apsystems/blob/master/dknr-apsystems_screenshot.png)](https://github.com/JcDenis/dknr-apsystems/blob/master/dknr-apsystems_screenshot.png)


## Fonctionnalités

- **Support de plusieurs ECU**.
- **Décodage des valeurs des ECU** et extraction des valeurs utiles.
- **Exploitation locale des mesures** pour le suivi de la consommation.
- **Intégration possible** dans une installation domotique ou un outil de supervision.


## Matériel requis

Le matériel exact dépend de l'installation, mais l'utilisation du projet nécessite généralement :

* une ou plusieurs unités APsystems ECU.
* une machine exécutant le logiciel docker et connectée au même réseau que les unités.

Ce projet a été testé avec une unité **ECU-C**. D'autres modules peuvent être supportés, si vous en connaissez ils peuvent être ajouté à cette liste.


## Installation

Des images Docker prêtes à l'emploi sont disponibles. 
Utilisez le fichier docker-compose.yaml à la racine du dépôt en fournissant les variables d'environnement suivantes :

* **DKNR_USERNAME** : login de l'interface node-red.
* **DKNR_PASSWORD** : mot de passe de l'interface node-red.
* **DKNR_SECRET**   : un mot secret pour encrypter les credits.


## A faire

* **Mode découverte** pour rechercher automatiquement les appareils sur le réseau local.
* **Support Home-Assistant** pour les messages MQTT
* N'afficher que les options disponibles suivant le modèle.


## Contribuer

Ce projet est **open-source**, vous pouvez participer en créant des [tickets](https://github.com/JcDenis/dknr-apsystems/issues) ou en proposant de [requêtes](https://github.com/JcDenis/dknr-apsystems/pulls) sur le dépôt github du projet.
