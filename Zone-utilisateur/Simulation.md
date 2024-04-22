---
title: Simulation
sidebar_position: 6
slug: /35f5b2b3-e0f5-4bd6-964e-b659f69d1075
---



Pour utiliser MiniPock dans un environnement simulé il est nécessaire d’avoir installé [Gz Sim Garden](https://gazebosim.org/docs/garden/install).

## Lancer la simulation {#f8e71f1231474120acda0b1515f6ca45}

Assurez vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

Lancez le bringup du MiniPock

```shell
ros2 launch minipock_bringup bringup.launch.py
```

Lancez ensuite la simulation

```shell
ros2 launch minipock_gz spawn.launch.py 
```

![](/img/161003219.png)

Vous pouvez ensuite lancer les autres stacks (téléopération, SLAM, navigation) pour utiliser le MiniPock.
