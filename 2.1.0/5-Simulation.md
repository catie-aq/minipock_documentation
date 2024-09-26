---
title: Simulation
---

Pour utiliser MiniPock dans un environnement simulé il est nécessaire d’avoir installé [Gz Sim Harmonic](https://gazebosim.org/docs/harmonic/install).

:::warning

Pour lancer la simulation, assurez-vous d'avoir installé [`gz-harmonic`](https://gazebosim.org/docs/harmonic/install_ubuntu) ou de lancer le container Docker avec l'image taggé simulation.

:::

## Lancer la simulation

:::info
Le [fichier de configuration de la flotte de minipock](https://github.com/catie-aq/minipock/blob/d142d3694b96a446592f0b822c336ed1964f9d7f/minipock/minipocks.yaml) doit être complété pour donner des informations pratiques aux différents composants comme la simulation ou la navigation.
:::

```shell
ros2 launch minipock_gz spawn.launch.py opt_param_1:=my_param
```

Les paramètres optionnels:

- **paused** (bool): Pour démarrer la simulation en pause.
- **world** (string): Nom du monde. Par défaut ***minipock_world***.

![](../img/multi_robot/multi_minipock.png)

Vous pouvez ensuite lancer les autres stacks (téléopération, SLAM, navigation) pour utiliser le MiniPock.

## API Documentation

### `/minipock_0/robot_state_publisher`

Responsable de la publication de l'état du robot.

- Subscribers:
  - `/clock` - `rosgraph_msgs/msg/Clock` : Horloge de la simulation
  - `/namespace/joint_states` - `sensor_msgs/msg/JointState` : État des joints du robot
- Publishers:
  - `/namespace/robot_description` - `std_msgs/msg/String` : Description du robot (URDF)
  - `/tf` - `tf2_msgs/msg/TFMessage` : Transformations entre les différents repères
  - `/tf_static` - `tf2_msgs/msg/TFMessage` : Transformations statiques

### `/ros_gz_bridge`

Responsable de la communication entre ROS et Gazebo.

- Subscribers:
  - `/clock` - `rosgraph_msgs/msg/Clock` : Horloge de la simulation
  - `/namespace/cmd_vel` - `geometry_msgs/msg/Twist` : Commande de vitesse du robot
- Publishers:
  - `/clock` - `rosgraph_msgs/msg/Clock` : Horloge de la simulation
  - `/namespace/joint_states` - `sensor_msgs/msg/JointState` : État des joints du robot
  - `/namespace/odom` - `nav_msgs/msg/Odometry` : Position du robot via l'odométrie
  - `/namespace/pose` - `tf2_msgs/msg/TFMessage` : Position du robot absolue
  - `/namespace/scan_raw` - `sensor_msgs/msg/LaserScan` : Données du lidar
  - `/tf` - `tf2_msgs/msg/TFMessage` : Transformations entre les différents repères

### `/scan_filter_node`

Responsable du filtrage des données du lidar.

- Subscribers:
  - `/clock` - `rosgraph_msgs/msg/Clock` : Horloge de la simulation
  - `/minipock_0/scan_raw` - `sensor_msgs/msg/LaserScan` : Données brutes du lidar
- Publishers:
  - `/minipock_0/scan` - `sensor_msgs/msg/LaserScan` : Données filtrées du lidar
