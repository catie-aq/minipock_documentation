---
title: Navigation
sidebar_position: 4
---

Ce package fournit l'implémentation de la stack de navigation 2 sur le robot MiniPock.

## Installation {#79d64bd3aaf042feb01d16e8000f95ab}

Pour installer ce package, assurez-vous que votre workspace ROS est correctement configuré.

```bash
cd <your_ros2_workspace>
colcon build --packages-select minipock_navigation2
```

## Utilisation en simulation {#edcb6ce69a71408185ba76fae1ebb038}

Pour utiliser ce package il est nécessaire de lancer la simulation gazebo du robot MiniPock installée via le package [minipock_gz](https://github.com/catie-aq/minipock_gz) en utilisant le launch file suivant:

```bash
ros2 launch minipock_gz minipock.launch.py
```

puis de lancer le launch file de navigation:

```bash
ros2 launch minipock_navigation2 navigation2.launch.py
```

## Configuration {#efdc531954184e9d9f35e9c06f2cc5d0}

La configuration de la stack de navigation se fait via le
fichier [minipock.yaml](https://github.com/catie-aq/minipock_navigation/blob/main/minipock_navigation2/param/minipock.yaml)
