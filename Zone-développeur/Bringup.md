---
title: Bringup
sidebar_position: 5
slug: /7750e0e4-54d5-4bc7-9d9f-4c220183cc15
---



_This documentation is auto-generated from_ [_catie-aq/minipock/README.md_](https://github.com/catie-aq/minipock)


# MiniPock Bringup {#0450c534089e475281e205f54c1676a8}

- Maintainer status: developed
- Maintainer: Sébastien Delpeuch [s.delpeuch@catie.fr](mailto:s.delpeuch@catie.fr)
- License: Apache 2.0
- Bug / feature tracker: [https://github.com/catie-aq/minipock_bringup/issues](https://github.com/catie-aq/minipock_bringup/issues)
- Source: git [https://github.com/catie-aq/minipock_bringup](https://github.com/catie-aq/minipock_bringup)

Ce package fournit l'implémentation du Bringup de la plateforme Minipock.


## Installation {#68a7d67ff67b499288bae2dde921b5b7}


Pour installer ce package, assurez-vous que votre workspace ROS est correctement configuré.


```bash
cd <your_ros2_workspace>
colcon build --packages-select minipock_bringup
```


## Utilisation {#0f8d08ebfcaf479abce8fd9449c04542}


Pour lancer le Bringup de la plateforme Minipock, il suffit de lancer la commande suivante :


```bash
ros2 launch minipock_bringup bringup.launch.py
```


Il est nécessaire d'être sur le même réseau que la plateforme Minipock pour pouvoir la contrôler. Le package est nécessaire pour lancer d'autres packages de la plateforme Minipock (hormis le package `minipock_teleop`).


## API Documentation {#2913071717c94233beed37115506e8d4}


### Noeuds {#704a267ec5864b6383b8a846e019e81e}

- `/joint_state_publisher`: Ce noeud recueille et publie l'état de tous les joints mobiles du robot.
- `/odometry_transform_publisher`: Ce noeud génère et publie les informations de transformation d'odométrie, qui comprennent la position et l'orientation du robot dans le repère du monde.
- `/robot_state_publisher`: Ce noeud publie l'intégralité de l'état (position et vitesse) du robot sur le sujet `/joint_states`.

### Topics {#2e32ff41cea44e8397afad15a020cdf9}

- `/joint_states`: Ce topic diffuse l'état de tous les joints mobiles du robot, y compris la position, la vitesse et l'effort appliqué.
- `/odom`: Ce topic publie les informations d'odométrie, y compris la position et la vitesse dans le repère du monde.
- `/robot_description`: Ce topic publie le URDF (Universal Robot Description Format) du robot, qui fournit des informations descriptives détaillées sur le modèle du robot.
- `/tf`: Le topic `/tf` publie les transformations entre les différents repères coordonnés dans le robot.
- `/tf_static`: Ce topic publie des informations de transformation statiques, qui contrairement à `/tf`, ne changent pas avec le temps.
