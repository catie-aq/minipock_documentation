---
title: Cartographer
sidebar_position: 11
---

Ce package fournit l'implémentation de la stack de navigation 2 sur le robot MiniPock.

## Installation

Pour installer ce package, assurez-vous que votre workspace ROS est correctement configuré.

```bash
cd <your_ros2_workspace>
colcon build --packages-select minipock_cartographer
```

## Utilisation

Pour utiliser ce package il est nécessaire de lancer la simulation gazebo du robot MiniPock :

:::danger

Pour fonctionner le fichier de configuration de la flotte `minipock/minipocks.yaml` doit être le suivant :

```yaml
namespace: minipock_
bringup: false
use_sim_time: true
fleet:
  "0":
    mode: differential
    position: null
```

:::

```bash
ros2 launch minipock_gz spawn.launch.py
```

puis de lancer cartographer:

```bash
ros2 launch minipock_cartographer cartographer.launch.py
```

Vous pouvez ensuite lancer le node de téléopération pour contrôler le robot:

```bash
ros2 run minipock_teleop teleop_keyboard
```

Une fois la carte construite, vous pouvez enrégistrer la carte dans un fichier `.pgm` et `.yaml` en utilisant le node

```bash
ros2 run nav2_map_server map_saver_cli -f <file_name>
```

## API Documentation

### Noeuds

- `/cartographer_node`: Ce noeud est responsable de la construction de la carte du robot MiniPock.
- `/cartographer_occupancy_grid_node`: Ce noeud est responsable de la publication de la carte de probabilité d'occupation.
- `rviz2` : Visualisation de la carte en temps réel.
- `odom_relay` : Relais de l'odométrie de `minipock_0/odom` à `odom` voir [documentation](https://google-cartographer-ros.readthedocs.io/en/latest/configuration.html)
- `scan_relay` : Relais des scans de `minipock_0/scan` à `scan` voir [documentation](https://google-cartographer-ros.readthedocs.io/en/latest/configuration.html)

### Topics

Publiés par `cartographer_node`:

- `/submap_list`: Ce topic diffuse la liste des submaps.
- `/trajectory_node_list`: Ce topic publie la liste des trajectoires.
- `/tf`: Le topic `/tf` publie les transformations entre les différents repères coordonnés dans le robot.
- `/contraint_list`: Ce topic publie les contraintes entre les différentes trajectoires.
- `/landmark_poses_list`: Ce topic publie les poses des landmarks.
- `/scan_matched_points2`: Ce topic publie les points de scan correspondants.

Publiés par `cartographer_occupancy_grid_node`:

- `/map`: Ce topic publie la carte de probabilité d'occupation.

Soucrit par `cartographer_node`:

- `/scan`: Ce topic reçoit les scans du lidar.
- `/odom`: Ce topic reçoit l'odométrie du robot.
