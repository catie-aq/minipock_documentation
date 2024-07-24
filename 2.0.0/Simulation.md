---
title: Simulation
sidebar_position: 7
---



Pour utiliser MiniPock dans un environnement simulé il est nécessaire d’avoir installé [Gz Sim Garden](https://gazebosim.org/docs/garden/install).

:::warning

Pour lancer la simulation, assurez-vous d'avoir installé [`gz-garden`](https://gazebosim.org/docs/garden/install_ubuntu) ou de lancer le container Docker avec `target=simulation`.

:::

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Lancer la simulation

Assurez vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

<Tabs>
<TabItem value="smmple robot" label="Version simple robot" default>

### Robot unique

Lancez ensuite la simulation

```shell
ros2 launch minipock_gz spawn.launch.py
```

![image](../img/161003219.png)

Vous pouvez ensuite lancer les autres stacks (téléopération, SLAM, navigation) pour utiliser le MiniPock.

</TabItem>

<TabItem value="multi robot" label="Version supportant le multi-robots">

### Multi-robots

Cette version permet de créer et afficher le nombre souhaité de minipocks.

```shell
ros2 launch minipock_gz spawn_multiple.launch.py use_sim_time:=true opt_param_1:=my_param
```

Les paramètres optionnels:

- **use_sim_time** (bool): Pour utiliser le temps de la simulation par défaut
- **nb_robots** (int): Nombre de robots souhaités. Par défaut ***1***.
- **robot_name** (string): Nom commun à tous les robots, un suffixe sera ajouté incrémentalement. *(exemple: minipock0, minipock1, minipock2, etc.)*. Par défaut ***minipock***.
- **world** (string): Nom du monde. Par défaut ***minipock_world***.

**Pour une utiisation couplée avec la navigation, mettre *use_sim_time* à *true***

![](../img/multi_robot/multi_minipock.png)

</TabItem>

</Tabs>
