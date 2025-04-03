---
title: Bringup
---

Ce package fournit l'implémentation du Bringup de la plateforme Minipock.

## Installation

Pour installer ce package, assurez-vous que votre workspace ROS est correctement configuré.

```bash
cd <your_ros2_workspace>
colcon build --packages-select minipock_bringup
```

## Utilisation

Pour lancer le Bringup de la plateforme Minipock, il suffit de lancer la commande suivante :

```bash
ros2 launch minipock_bringup bringup.launch.py
```

Il est nécessaire d'être sur le même réseau que la plateforme Minipock pour pouvoir la contrôler. Le package est nécessaire pour lancer d'autres packages de la plateforme Minipock (hormis le package `minipock_teleop`).

## API Documentation

La documentation de l'API est divisée en deux parties :

- L'API créée par la plateforme via Micro-ROS
- L'API créée par le Bringup sur le PC

Le namespace est propre à chaque plateforme MiniPock, par défaut `minipock_0`.

### API MiniPock

API de la plateforme matérielle MiniPock.

#### `/namespace`

Noeud micro-ROS s'executant sur la plateforme Minipock

- Subscribers:
  - `/namespace/cmd_vel` - `geometry_msgs/msg/Twist` : Commande de vitesse du robot
- Publishers:
  - `/namespace/odom_raw` - `geometry_msgs/msg/PoseStamped` : Position du robot
  - `/namespace/scan_raw` - `sensor_msgs/msg/LaserScan` : Données du lidar

### API Bringup

#### `/namespace/joint_state_publisher`

Responsable de la publication de l'état des joints du robot.

- Subscribers:
  - `/namespace/robot_description` - `std_msgs/msg/String` : Description du robot (URDF)
- Publishers:
  - `/namespace/joint_states` - `sensor_msgs/msg/JointState` : État des joints du robot

#### `/namespace/raw_data_transformer`

Responsable de la transformation des données brutes de la plateforme MiniPock.

- Subscribers:
  - `/namespace/odom_raw` - `geometry_msgs/msg/PoseStamped` : Position du robot
  - `/namespace/scan_raw` - `sensor_msgs/msg/LaserScan` : Données du lidar

- Publishers:
  - `/namespace/odom` - `nav_msgs/msg/Odometry` : Position du robot (traitée)
  - `/namespace/scan` - `sensor_msgs/msg/LaserScan` : Données du lidar (traitées)
  - `/tf` - `tf2_msgs/msg/TFMessage` : Transformations entre les différents repères
