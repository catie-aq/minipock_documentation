---
title: Navigation
sidebar_position: 5
---



La navigation consiste à déplacer le robot d'un endroit à la destination spécifiée dans un environnement donné. Pour ce faire, une carte contenant des informations géométriques sur les meubles, les objets et les murs de l'environnement donné est nécessaire. Comme décrit dans la section SLAM précédente, la carte a été créée avec les informations de distance obtenues par le capteur et les informations de pose du robot lui-même.

La navigation permet à un robot de se déplacer de la position actuelle à la position cible désignée sur la carte en utilisant la carte, l'encodeur du robot, le capteur IMU et le capteur de distance. La procédure d'exécution de cette tâche est la suivante.

## Lancement de la navigation {#9fc2d811ea2d41768c782ec5cec8e1bf}

Assurez vous d’être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`)

Lancez la navigation

```shell
ros2 launch minipock_navigation2 navigation2.launch.py 
```

Si l'environnement est simulé il faut lancer

```shell
ros2 launch minipock_navigation2 navigation2.launch.py bringup:=false use_sim_time:=true
```

La `map` utilisée est le fichier `map.yaml` dans `minipock_navigation2/map/map.yaml`

Lorsque Rviz sera ouvert cliquez sur “Startup” dans l’onglet de navigation 2 pour lancer la stack de navigation

## Estimer la position initiale {#c2321eafe318407bb862d107bf6016b0}

L'estimation initiale de la pose doit être effectuée avant de lancer la navigation, car ce processus initialise les paramètres AMCL qui sont essentiels à la navigation. MiniPock doit être correctement localisé sur la carte avec les données du capteur LDS qui se superposent parfaitement à la carte affichée.

- Cliquez sur le bouton 2D Pose Estimate dans le menu RViz2.
- Cliquez sur la carte où se trouve le robot et faites glisser la grande flèche verte vers la direction à laquelle le robot fait face.

## Donner un ordre de navigation {#bf4026c011e3480aba7be41efbe2dd03}

- Cliquez sur le bouton Navigation2 Goal dans le menu RViz2.
- Cliquez sur la carte pour définir la destination du robot et faites glisser la flèche verte vers la direction vers laquelle le robot sera orienté.
  - Cette flèche verte est un marqueur qui permet de spécifier la destination du robot.
  - La racine de la flèche correspond aux coordonnées x, y de la destination, et l'angle θ est déterminé par l'orientation de la flèche.
  - Dès que x, y, θ sont définis, TurtleBot3 commence immédiatement à se déplacer vers la destination.

![](../img/1887772889.png)

## Paramétrage {#2d7fb3cd591b41c4b090ea7fde2b5039}

Les paramètres de navigation sont paramétrables dans le fichier [`minipock.yaml`](https://github.com/catie-aq/minipock_navigation/blob/main/minipock_navigation2/param/minipock.yaml) en suivant le [Guide de paramétrage](https://navigation.ros.org/tuning/index.html).
