---
title: Navigation
sidebar_position: 6
---



La navigation consiste à déplacer le robot d'un endroit à la destination spécifiée dans un environnement donné. Pour ce faire, une carte contenant des informations géométriques sur les meubles, les objets et les murs de l'environnement donné est nécessaire. Comme décrit dans la section SLAM précédente, la carte a été créée avec les informations de distance obtenues par le capteur et les informations de pose du robot lui-même.

La navigation permet à un robot de se déplacer de la position actuelle à la position cible désignée sur la carte en utilisant la carte, l'encodeur du robot, le capteur IMU et le capteur de distance. La procédure d'exécution de cette tâche est la suivante.

## Lancement de la navigation

Assurez vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
<TabItem value="real" label="Réel" default>

```shell
ros2 launch minipock_navigation2 navigation2.launch.py
```

</TabItem>

<TabItem value="simulation" label="Simulation">

```shell
ros2 launch minipock_navigation2 navigation2.launch.py bringup:=false use_sim_time:=true
```

</TabItem>

<TabItem value="simulation_multiple" label="Simulation Multi-robot">

Il est possible de **lancer navigation et localisation en forçant le démarrage** grâce à:
```bash
ros2 launch minipock_navigation2 navigation2_multiple.launch.py bringup:=false use_sim_time:=true autostart:=true nb_robots:=nb_robots robot_name:=robot_name
```
Les paramètres optionnels:
- **nb_robots** (int): Nombre de robots souhaités. Par défaut ***1***.
- **robot_name** (string): Nom commun à tous les robots, un suffixe sera ajouté incrémentalement. *(exemple: minipock0, minipock1, minipock2, etc.)*. Par défaut ***minipock***.
- **start_rviz** (bool): Démarrage automatique de rviz. Par défaut ***true***.
- **use_sim_time** (bool): Pour utiliser le temps de la simulation (**recommandé**). Par défaut ***false*** .
- **bringup** (bool): Démarrage du bringup de minipock. Par défaut ***true***.
- **autostart** (bool): Démarrage automatique des éléments de navigation. Par défaut ***false***.
- **use_composition** (bool): Les nodes sont lancés dans des containers afin d'optimiser la mémoire et les ressources CPU utilisées. Par défaut ***true***.
- **use_respawn** (bool): Relance les nodes qui plantent. À utiliser si la composition est désactivée. Par défaut: ***false***.
</TabItem>

</Tabs>

La `map` utilisée est le fichier `map.yaml` dans `minipock_navigation2/map/map.yaml`

Lorsque Rviz sera ouvert cliquez sur “Startup” dans l’onglet de navigation 2 pour lancer la stack de navigation

## Estimer la position initiale

L'estimation initiale de la pose doit être effectuée avant de lancer la navigation, car ce processus initialise les paramètres AMCL qui sont essentiels à la navigation. MiniPock doit être correctement localisé sur la carte avec les données du capteur LDS qui se superposent parfaitement à la carte affichée.

- Cliquez sur le bouton 2D Pose Estimate dans le menu RViz2.
- Cliquez sur la carte où se trouve le robot et faites glisser la grande flèche verte vers la direction à laquelle le robot fait face.

## Donner un ordre de navigation

- Cliquez sur le bouton Navigation2 Goal dans le menu RViz2.
- Cliquez sur la carte pour définir la destination du robot et faites glisser la flèche verte vers la direction vers laquelle le robot sera orienté.
  - Cette flèche verte est un marqueur qui permet de spécifier la destination du robot.
  - La racine de la flèche correspond aux coordonnées x, y de la destination, et l'angle θ est déterminé par l'orientation de la flèche.
  - Dès que x, y, θ sont définis, TurtleBot3 commence immédiatement à se déplacer vers la destination.

![image](../img/1887772889.png)

## Paramétrage

Les paramètres de navigation sont paramétrables dans le fichier [`minipock.yaml`](https://github.com/catie-aq/minipock_navigation/blob/main/minipock_navigation2/param/minipock.yaml) en suivant le [Guide de paramétrage](https://navigation.ros.org/tuning/index.html).

___

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
ros2 launch minipock_navigation2 navigation2_multiple.launch.py bringup:=false use_sim_time:=true autostart:=true nb_robots:=nb_robots robot_name:=robot_name
```
Les paramètres optionnels:
- **nb_robots** (int): Nombre de robots souhaités. Par défaut ***1***.
- **robot_name** (string): Nom commun à tous les robots, un suffixe sera ajouté incrémentalement. *(exemple: minipock0, minipock1, minipock2, etc.)*. Par défaut ***minipock***.
- **start_rviz** (bool): Démarrage automatique de rviz. Par défaut ***true***.
- **use_sim_time** (bool): Pour utiliser le temps de la simulation (**recommandé**). Par défaut ***false*** .
- **bringup** (bool): Démarrage du bringup de minipock. Par défaut ***true***.
- **autostart** (bool): Démarrage automatique des éléments de navigation. Par défaut ***false***.
- **use_composition** (bool): Les nodes sont lancés dans des containers afin d'optimiser la mémoire et les ressources CPU utilisées. Par défaut ***true***.
- **use_respawn** (bool): Relance les nodes qui plantent. À utiliser si la composition est désactivée. Par défaut: ***false***.
</TabItem>

</Tabs>

## Configuration {#efdc531954184e9d9f35e9c06f2cc5d0}

La configuration de la stack de navigation se fait via le
fichier [minipock.yaml](https://github.com/catie-aq/minipock_navigation/blob/main/minipock_navigation2/param/minipock.yaml)
