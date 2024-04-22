---
title: Téléopération
sidebar_position: 2
slug: /239ab349-ad18-4af6-88e7-d016bcb4564c
---



_This documentation is auto-generated from_ [_catie-aq/minipock/README.md_](https://github.com/catie-aq/minipock)

# MiniPock Keyboard Teleoperation {#e267ca6de1c94fa0ab6d1cd7311d4bff}

Ce package fournit un moyen de contrôler le robot MiniPock. Il a été créé pour être utilisé avec ROS 2. Il permet de
commander le mouvement linéaire et angulaire du robot à l'aide des touches de clavier suivantes : `z`, `q`, `s`, `d` et `x`.

## Installation {#22eb8b7d3b64457f8100e65359ca033c}

Pour installer ce package, assurez-vous que votre workspace ROS est correctement configuré.

```bash
cd <your_ros2_workspace>
colcon build --packages-select minipock_teleop
```

Ce package dépend des packages rclpy et geometry_msgs.msg. Veuillez vous assurer qu'ils sont installés dans votre
environnement.

## Utilisation {#ff82eb6a65bd4dfe901c8d903cc2666e}

Pour utiliser ce package, vous pouvez exécuter le script Python à partir de la ligne de commande:

```bash
ros2 run minipock_teleop teleop_keyboard
```
