---
title: Démarrage rapide
sidebar_position: 4
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

```bash
ros2 run minipock_teleop teleop_keyboard --ros-args -p namespace:=robot_namespace/
```

-> *En cas de mauvais namespace demandé la liste des namespaces existants sera donnée*
-> *Dans le cas où le topic cmd_vel demandé n'existerait pas, la liste des topics cmd_vel existants sera donnée*

</TabItem>

</Tabs>

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

## Configuration de la flotte

La configuration de la flotte se fait dans le fichier `minipock/minipocks.yaml`

```yaml
namespace: minipock_ # pattern de nommage des namespaces minipock_0, minipock_1, ...
bringup: false # true en cas de robot réel
use_sim_time: true # false en cas de robot réel
fleet:
  "0": # nom du robot
    mode: differential # mode de contrôle differential ou holonomic
    position: null # position initiale du robot null pour aléatoire
```

Lorsque plusieurs robots sont spécifiés dans le fichier de configuration, les différents robots sont lancés avec le namespace spécifié dans le fichier de configuration et un numéro incrémenté à la fin du namespace.

:::warning

Dans le cas des robots réels chaque robot possède un namespace et un numéro unique, il faut donc avoir un fichier cohérent avec la configuration des robots réels

:::

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
