---
title: Multiple Robots
sidebar_position: 7
---

L'utilisation de plusieurs robots au sein d'une même simulation reprends la logique des différents guides précedents: l'[**installation**](Installation.md), le [**démarrage rapide**](Démarrage-rapide.md), la [**navigation**](Navigation.md) et la [**simulation**](Simulation.md).

Cependant les configurations changent et des fichiers de lancement adaptés sont à utiliser pour la simuation et la navigation.

## [Simulation](Simulation.md)

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

***<p style="text-align: center;">![](../../img/multi_robot/multi_minipock.png)</p>***

![](../../img/multi_robot/multi_minipock.png)

## Téléopération

```bash
ros2 run minipock_teleop teleop_keyboard --ros-args -p namespace:=robot_namespace/
```
-> *En cas de mauvais namespace demandé la liste des namespaces existants sera donnée*
-> *Dans le cas où le topic cmd_vel demandé n'existerait pas, la liste des topics cmd_vel existants sera donnée*


## [Navigation](Navigation.md)

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


Une fenêtre rviz se lancera automatiquement sans nécessité de startup manuel.