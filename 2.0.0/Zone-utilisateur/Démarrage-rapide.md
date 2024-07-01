---
title: Démarrage rapide
sidebar_position: 3
---

## Démarrer MiniPock 🚀

:::warning

Ce guide suppose que vous avez un MiniPock flashé prêt à l'emploi

:::

Assurez-vous d’être connecté au même réseau que le MiniPock avec votre PC

## Téléopération

Assurez vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

Lancez ensuite le noeud de téléopération

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
<TabItem value="standalone" label="Robot Unique" default>

```shell
ros2 run minipock_teleop teleop_keyboard
```

</TabItem>

<TabItem value="multiple" label="Plusieurs robots">

```shell
ros2 run minipock_teleop teleop_keyboard --ros-args -p namespace:=robot_namespace/
```

</TabItem>

Suivez ensuite les indications du terminal

```shell
Control Your MiniPock!
---------------------------
Moving around:
        z
   q    x    d
        s

z/s : increase/decrease linear velocity
q/d : increase/decrease angular velocity

x : force stop

CTRL-C to quit
```

## Bringup

:::danger

Ce noeud est nécessaire **uniquement** pour manipuler le robot réel. Il est automatiquement lancé par la stack de navigation lorsqu'elle est utilisée

:::

Le bringup permet de lancer les noeud de base du MiniPock comme le `robot_state_publisher`,

Assurez-vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

```shell
ros2 launch minipock_bringup bringup.launch.py
```

Assurez-vous de conserver ce terminal ouvert pour lancer une stack (hormis la téléopération)
