---
title: Démarrage rapide
sidebar_position: 3
---



## Démarrer MiniPock 🚀 {#bbbde3b86d824d01a98ad75313615caa}

Configuration par défaut :

- ROS domain ID : 10
- Micro-ROS agent baudrate : 460800

Assurez-vous d’être connecté au même réseau que le MiniPock avec votre PC

## Téléopération {#9fa4cec3ac414b8bb55229ac3283074a}

Assurez vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

Lancez ensuite le noeud de téléopération

```shell
ros2 run minipock_teleop teleop_keyboard
```

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

## Bringup {#5943dcb3269b49bea680ff7a32b1fdd7}

Le bringup permet de lancer les noeud de base du MiniPock comme le `robot_state_publisher`,

Assurez-vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

```shell
ros2 launch minipock_bringup bringup.launch.py
```

Assurez-vous de conserver ce terminal ouvert pour lancer une stack (hormis la téléopération)
