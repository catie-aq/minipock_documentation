---
title: Gz Sim
sidebar_position: 1
---



_This documentation is auto-generated from_ [_catie-aq/minipock/README.md_](https://github.com/catie-aq/minipock)

# MiniPock Gazebo {#67d61bf22e8d482c9c8e4f1a181ba0e1}

- Maintainer status: developed
- Maintainer: Sébastien Delpeuch [s.delpeuch@catie.fr](mailto:s.delpeuch@catie.fr)
- License: Apache 2.0
- Bug / feature tracker: [https://github.com/catie-aq/minipock_gz/issues](https://github.com/catie-aq/minipock_gz/issues)
- Source: git [https://github.com/catie-aq/minipock_gz](https://github.com/catie-aq/minipock_gz)

Ensemble de ressources permettant de configurer l'environnement de simulation Gazebo ainsi que les plugins ROS
nécessaires dans le cadre du projet MiniPock.
Ce package configure par ailleurs les différents bridges nécessaires pour la communication entre ROS 2 Humble et Gazebo
Sim .

## Description du monde {#96512d89e5af4ac98755fe94ec6afed4}

Le monde est défini en se basant sur [https://app.gazebosim.org/OpenRobotics/fuel/worlds/industrial-warehouse](https://app.gazebosim.org/OpenRobotics/fuel/worlds/industrial-warehouse) permettant
de simuler un entrepôt industriel. Il est adapté dans le
fichier [https://github.com/catie-aq/minipock_gz/blob/main/worlds/minipock_world.sdf](https://github.com/catie-aq/minipock_gz/blob/main/worlds/minipock_world.sdf). Hormis les plugins classiques
ci-dessous aucun plugin particulier n’est présent dans la simulation

[https://github.com/catie-aq/minipock_gz/blob/383f44e21df04b010668e603d954344cc94b5f56/worlds/minipock_world.sdf#L468-L497](https://github.com/catie-aq/minipock_gz/blob/383f44e21df04b010668e603d954344cc94b5f56/worlds/minipock_world.sdf#L468-L497)

La simulation est chargée via le launch file [https://github.com/catie-aq/minipock_gz/blob/main/launch/spawn.launch.py](https://github.com/catie-aq/minipock_gz/blob/main/launch/spawn.launch.py)
plus particulièrement la fonction `simulation` permettant de lancer `gz-sim` et de charger `minipock_world.sdf`et la
fonction `spawn` permettant de convertir l’entrée `URDF` de [https://github.com/catie-aq/minipock_description](https://github.com/catie-aq/minipock_description) en un `sdf`
en s’appuyant sur les scripts fournis.

## Communication ROS2 ↔ Gazebo Sim {#5225fbecf8004b12b9ca22ff504e5716}

Le projet utilise [https://github.com/gazebosim/ros_gz/tree/humble/ros_gz_bridge](https://github.com/gazebosim/ros_gz/tree/humble/ros_gz_bridge) pour transmettre les données de
simulation à ROS2. Les différents bridges sont disponibles
dans [https://github.com/catie-aq/minipock_gz/blob/main/minipock_gz/bridges.py](https://github.com/catie-aq/minipock_gz/blob/main/minipock_gz/bridges.py). Un résumé des noeuds disponible est
extrait ci dessous

Le package fournit aussi `minipock.rviz` permettant de visualiser les données disponibles

Un noeud spécifique `scan_filter_node` est créé.

Ce module Python introduit une classe nommée ScanFilterNode liée à ROS2. Cette classe représente un nœud dans un système
ROS2 et fournit des fonctionnalités pour écouter les messages provenant du topic `/minipock/scan_raw` et les publier
dans le topic `/minipock/scan`, après avoir modifié l'identifiant du cadre (`frame_id`).
La classe `ScanFilterNode` hérite de la classe Node qui est un composant central de la bibliothèque `rclpy`.

### Classe ScanFilterNode {#77658d53da834dd98c5d207bd9181a34}

La méthode **init** crée une instance de la classe. Pendant l'initialisation, elle crée un nœud nommé '
scan_filter_node', configure une souscription au topic `/minipock/scan_raw` et crée un éditeur pour `/minipock/scan`,
tous avec une taille de file d'attente de 10.
`listener_callback` est une méthode qui modifie l'identifiant du cadre (`frame_id`) des messages `LaserScan` entrants et
utilise l'éditeur pour les envoyer à `/minipock/scan`.
