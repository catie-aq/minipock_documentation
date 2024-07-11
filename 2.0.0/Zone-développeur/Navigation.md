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

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
<TabItem value="simulation" label="Simulation">

```bash
ros2 launch minipock_gz minipock.launch.py
```

puis de lancer le launch file de navigation:

```shell
ros2 launch minipock_navigation2 navigation2.launch.py bringup:=false use_sim_time:=true
```

</TabItem>

<TabItem value="simulation_multiple" label="Simulation Multi-robot">

```shell
ros2 launch minipock_gz spawn_multiple.launch.py use_sim_time:=true opt_param_1:=my_param
```

Puis il est possible de **lancer navigation et localisation en forçant le démarrage** grâce à:

```bash
ros2 launch minipock_navigation2 navigation2_multiple.launch.py bringup:=false use_sim_time:=true autostart:=true
```
</TabItem>

</Tabs>

## Configuration {#efdc531954184e9d9f35e9c06f2cc5d0}

La configuration de la stack de navigation se fait via le
fichier [minipock.yaml](https://github.com/catie-aq/minipock_navigation/blob/main/minipock_navigation2/param/minipock.yaml)
