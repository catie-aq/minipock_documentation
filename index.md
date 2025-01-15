---
sidebar_position: 1
---

# MiniPock

import DocCardList from '@theme/DocCardList';

<DocCardList />

## Changelog

Le projet MiniPock est constitué de trois blocs principaux chacun versionnés selon son propre cycle de vie au format [SemVer](https://semver.org/).

- [La mécanique et l'électronique](https://www.dropbox.com/home/SONU/Projets/RD25%20-%20Capteurs%20et%20Sys.%20TR%20pour%20la%20Robotique/MiniPOCK)
- [Le logiciel embarqué](https://github.com/catie-aq/minipock_zephyr-demo/releases)
- [Les packages ROS](https://github.com/catie-aq/minipock/releases)

La version du projet MiniPock suit son propre versionnage. Pour chaque version de MiniPock, les versions des trois blocs principaux sont indiquées.

### 2.2.0

| Mécanique et électronique | Logiciel embarqué | Packages ROS |
| -------------------------- | ----------------- | ------------ |
| [2.0.0](https://www.dropbox.com/home/SONU/Projets/RD25%20-%20Capteurs%20et%20Sys.%20TR%20pour%20la%20Robotique/MiniPOCK/plateforme%206tron%20V2) | [2.2.0](https://github.com/catie-aq/minipock_zephyr-demo/releases/tag/v2.1.0) | [2.2.0](https://github.com/catie-aq/minipock/releases/tag/2.1.0) |

- Ajout de la mise à jour du firmware via micro-ROS
- Reconnexion automatique à l'agent micro-ROS
- Stockage des paramètres (SSID, mot de passe, IP, namespace) dans la mémoire flash
- Ajout de commande shell pour la mise à jour et la configuration des paramètres

### 2.1.0

| Mécanique et électronique | Logiciel embarqué | Packages ROS |
| -------------------------- | ----------------- | ------------ |
| [2.0.0](https://www.dropbox.com/home/SONU/Projets/RD25%20-%20Capteurs%20et%20Sys.%20TR%20pour%20la%20Robotique/MiniPOCK/plateforme%206tron%20V2) | [2.1.0](https://github.com/catie-aq/minipock_zephyr-demo/releases/tag/v2.1.0) | [2.1.0](https://github.com/catie-aq/minipock/releases/tag/2.1.0) |

- Suppression de la Raspberry Pi sur la plateforme
- Ajout de la communication WiFi avec les stack 6TRON
- Ajotu des robots multiples (namespace)
- Ajout de la description holonome dans le package ROS
- Ajout du Agent Micro ROS dans le bringup
- Mise à jour de la téléopération pour avoir un mode FPS
- Mise à jour de la CI/CD pour construire automatiquement les images Docker

### 2.0.0

| Mécanique et électronique | Logiciel embarqué | Packages ROS |
| -------------------------- | ----------------- | ------------ |
| [2.0.0](https://www.dropbox.com/home/SONU/Projets/RD25%20-%20Capteurs%20et%20Sys.%20TR%20pour%20la%20Robotique/MiniPOCK/plateforme%206tron%20V2) | [2.0.0](https://github.com/catie-aq/minipock_zephyr-demo/releases/tag/v2.0.0) | [2.0.0](https://github.com/catie-aq/minipock/releases/tag/2.0.0) |

- Simplification du montage et démontage des plaques supérieures et inférieures
- Augmentation du nombre de stacks 6TRON dans la plateforme
- Réduction de l'encombrement des blocs moteurs
- Unification des pièces entre la version Holonome et la version Différentielle
- Augmentation de la hauteur de la plateforme
- Mise à jour de la description du robot dans les packages ROS

### 1.0.0

| Mécanique et électronique | Logiciel embarqué | Packages ROS |
| -------------------------- | ----------------- | ------------ |
| [1.0.0](https://www.dropbox.com/home/SONU/Projets/RD25%20-%20Capteurs%20et%20Sys.%20TR%20pour%20la%20Robotique/MiniPOCK/plateforme%206tron%20V1) | [1.0.0](https://github.com/catie-aq/minipock_zephyr-demo/releases/tag/1.0.0) | [1.0.0](https://github.com/catie-aq/minipock/releases/tag/1.0.0) |

Release initale
