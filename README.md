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
- **Support Home-Assistant Discovery** pour les messages MQTT
- **Historique de production solaire** enregistré dans InfluxDB : énergie produite par heure, par jour, par mois et par an.


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

### Historique (production solaire, InfluxDB)

Le fichier docker-compose démarre aussi un conteneur **InfluxDB 2** (`dknr_apsystems_influxdb`) qui conserve les valeurs relevées sans limite de durée. La page **Historique** du tableau de bord affiche l'énergie produite par heure (24 dernières heures), par jour (7 derniers jours), par mois (12 derniers mois) et par an.

Aucune variable supplémentaire n'est obligatoire : par défaut, dknr-apsystems utilise le conteneur InfluxDB du docker-compose. Les variables suivantes sont optionnelles :

| Variable | Valeur par défaut | Rôle |
|---|---|---|
| **DKNR_INFLUX_TOKEN** | `dknr-apsystems-influxdb-token` | jeton d'API InfluxDB |
| **DKNR_INFLUX_URL** | `http://dknr_apsystems_influxdb:8086` | adresse de la base InfluxDB |
| **DKNR_INFLUX_ORG** | `dknr` | organisation InfluxDB |
| **DKNR_INFLUX_BUCKET** | `apsystems` | bucket InfluxDB |

Au premier démarrage, InfluxDB est initialisé avec l'utilisateur **DKNR_USERNAME** et le mot de passe **DKNR_PASSWORD**, qui doit faire **8 caractères minimum**.

Quelques remarques :

* Le jeton par défaut convient tant qu'InfluxDB reste sur le réseau interne de docker. Si vous exposez le port 8086 (lignes commentées dans le docker-compose), définissez votre propre **DKNR_INFLUX_TOKEN**, par exemple généré avec `openssl rand -hex 32`.
* Le jeton, l'organisation et le bucket ne sont appliqués par InfluxDB qu'à sa **première** initialisation. Pour les changer ensuite, il faut supprimer le volume `dknr_apsystems_influxdb` (et donc l'historique) ou les modifier dans l'interface d'InfluxDB.
* Pour utiliser une base InfluxDB 2 existante, renseignez ces quatre variables pour le conteneur dknr_apsystems ; le conteneur InfluxDB du docker-compose (et le `depends_on` qui y fait référence) peut alors être retiré.
* La production est calculée à partir des compteurs de l'ECU (relevés toutes les 5 minutes) : `energy_today` pour les heures, plus précis, et `energy_total` pour les jours, mois et années. L'historique commence à la mise en place de la base, les données antérieures de l'ECU ne sont pas importées.


## A faire

* **Mode découverte** pour rechercher automatiquement les appareils sur le réseau local.
* N'afficher que les options disponibles suivant le modèle.


## Contribuer

Ce projet est **open-source**, vous pouvez participer en créant des [tickets](https://github.com/JcDenis/dknr-apsystems/issues) ou en proposant de [requêtes](https://github.com/JcDenis/dknr-apsystems/pulls) sur le dépôt github du projet.


## Voir aussi

- [DKNR Teleinfo](https://github.com/JcDenis/dknr-teleinfo)
- [DKNR APSystems](https://github.com/JcDenis/dknr-apsystems)
- [DKNR Daikin](https://github.com/JcDenis/dknr-daikin)
