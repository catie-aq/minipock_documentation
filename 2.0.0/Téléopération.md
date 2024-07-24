---
title: Téléopération
sidebar_position: 10
---


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

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
<TabItem value="standalone" label="Robot Unique" default>

```shell
ros2 run minipock_teleop teleop_keyboard
```

</TabItem>

<TabItem value="multiple" label="Plusieurs robots">

```bash
ros2 run minipock_teleop teleop_keyboard --ros-args -p namespace:=robot_namespace/
```
-> *En cas de mauvais namespace demandé la liste des namespaces existants sera donnée*
-> *Dans le cas où le topic cmd_vel demandé n'existerait pas, la liste des topics cmd_vel existants sera donnée*


</TabItem>

</Tabs>