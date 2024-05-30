---
title: Installation
sidebar_position: 2
---

## Prérequis 📦

- Installer [Ubuntu 22.04 LTS](https://ubuntu.com/download/raspberry-pi)
- Installer [ROS2 humble](https://docs.ros.org/en/humble/Installation.html)
- Installer docker [optionnel]

## Installation sur le PC 🖥

Créér un workspace ROS2 et cloner les dépôts MiniPock

```shell
mkdir -p ~/colcon_ws/src
cd ~/colcon_ws/src
git clone git@github.com:catie-aq/minipock.git
git clone -b humble https://github.com/micro-ROS/micro_ros_setup.git
```

Mettre à jour les dépendances avec `rosdep`

```bash
sudo apt update && rosdep update
rosdep install --from-paths src --ignore-src -y
```

Compiler le workspace

```shell
cd ~/colcon_ws
colcon build --merge-install
source install/setup.bash
ros2 run micro_ros_setup create_agent_ws.sh
colcon build --merge-install
source install/setup.bash
```

:::info

Une image docker peut être utilisée pour lancer l’agent Micro-ROS (debug et tests)

Documentation officielle : [https://micro.ros.org/docs/tutorials/core/first_application_rtos/zephyr/](https://micro.ros.org/docs/tutorials/core/first_application_rtos/zephyr/)

```bash
docker run -it --rm --env ROS_DOMAIN_ID=10 -v /dev:/dev --privileged --net=host microros/micro-ros-agent:humble udp4 --port 8888
```

:::

## Installation de la Stack Applicative | Micro ROS 🪁

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

## Installation stack Contrôle moteurs 

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