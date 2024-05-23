---
title: Installation
sidebar_position: 2
slug: /cc2c36ac-dc0a-4353-9ae7-c1ba6db37cba
---



## **Raspberry Pi** {#213c2b634b9f47bfbbdc7df423f5ae1e}

:::note

Identifiant de la RPi : **User** : turtlebot | **Password** : minipock

:::

- Installer [Ubuntu 22.04 LTS](https://ubuntu.com/download/raspberry-pi)
- Installer [ROS2 humble](https://docs.ros.org/en/humble/Installation.html)
- Installer docker [optionnel]

### Micro ROS agent {#47b6f070ab164e5ea3b60fd1e14d3b6b}

Une image docker peut être utilisée pour lancer l’agent Micro-ROS.

:::info

Documentation officiel : [https://micro.ros.org/docs/tutorials/core/first_application_rtos/zephyr/](https://micro.ros.org/docs/tutorials/core/first_application_rtos/zephyr/)

:::

- Dépendances Python :
 	- python3-rosdep2
 	- python3-vcstool
- Créer le workspace et télecharger Micro-ROS

```bash
mkdir microros_ws
cd microros_ws
git clone -b humble https://github.com/micro-ROS/micro_ros_setup.git src/micro_ros_setup
```

Mettre à jour les dépendances avec `rosdep`

```bash
sudo apt update && rosdep update
rosdep install --from-paths src --ignore-src -y
```

Compiler micro-ROS

```bash
colcon build
source install/local_setup.bash
```

Télécharger micro-ROS-Agent

```bash
ros2 run micro_ros_setup create_agent_ws.sh
```

Compiler

```bash
ros2 run micro_ros_setup build_agent.sh
source install/local_setup.bash
```

### Driver LiDAR {#d1a708442d874560a6369a5975671bb8}

Installer le driver du LiDAR LDS-01 depuis `apt`

```shell
sudo apt install ros-humble-hls-lfcd-lds-driver
```

## Stack Applicative | Micro ROS 🪁 {#e1b70e77fa434952942b30b511f5b700}

:::info

Module officiel µROS : [https://github.com/micro-ROS/micro_ros_zephyr_module.git](https://github.com/micro-ROS/micro_ros_zephyr_module)

:::

L’application de la stack applicative est basée sous Zephyr OS. L’application doit exposer un nœud ROS afin de pourvoir interagir avec un environnement ROS2.

### Dépendances {#45397276e5024c74bfe840680862fe61}

- Installer les [outils Zephyr OS](https://docs.zephyrproject.org/latest/develop/getting_started/index.html)

## Installation {#85e0637d9d67419dbce9bc52312cfef8}

- Initialiser le workspace Zephyr

```bash
west init -m https://github.com/catie-aq/zephyr_minipock minipock
cd minipock
west update
```

- Compiler l’application de base

```bash
west build -b zest_core_stm32l4a6rg app/base-application
```

- Flasher la carte

```bash
west flash
```

## Stack Contrôle moteurs {#a713aabb28334362a9aed529aa0bb41c}

L’application de contrôle moteur est basée sous Mbed OS.

### Dépendances {#2d14f162b5f549c1b0284cd56392767c}

- Installer les [outils Mbed OS](https://6tron.catie-lab.net/ressources_logicielles/mbed/)

### Installation {#fbec217e749943ce9b9b04c154b04666}

- Téléchargement l’application

```bash
git clone https://github.com/catie-aq/minipock_mbed-rbdc.git
cd minipock_mbed-rbdc
```

- Déployer les dépendances

```bash
mbed deploy
```

- Compiler et flasher

```bash
mbed compile
sixtron flash
```

:::tip

MINIPOCK_MAX_LIN_VEL = 2.0
MINIPOCK_MAX_ANG_VEL = 12.0

:::

## Démarrer le MiniPock 🚀 {#d4d4428548df478cb3310cab31e67c22}

Configuration par défaut :

- ROS domain ID : 10

### 
- Baudrate : 460800

Lancer le `micro-ROS` agent afin d’établir le lien avec l’environnement ROS2.

- Système

```bash
ros2 run micro_ros_agent micro_ros_agent serial --baudrate=460800 --dev [/dev/ttyUSBx]
ros2 launch hls_lfcd_lds_driver hlds_laser.launch.py port:=[/dev/ttyUSBx] frame_id:=lds_01_link
```

- Docker

```bash
docker run -it --rm --env ROS_DOMAIN_ID=10 -v /dev:/dev --privileged --net=host microros/micro-ros-agent:humble serial --dev /dev/ttyUSB0 --baudrate 460800 -v6
```

## Configuration du PC {#4f4fbcdfd052475497982b3ff0ae45cb}

Dans un workspace ROS2 il est nécessaire de cloner les différents dépôts MiniPock

```shell
cd <your_workspace>/src
git clone git@github.com:catie-aq/minipock.git
cd ..
colcon build --merge-install
source install/setup.bash
```

Toutes les opérations doivent être réalisées en étant connecté au même Wi-Fi que le MiniPock
