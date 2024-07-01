---
title: Installation
sidebar_position: 2
---

## Prérequis 📦

- Installer [Ubuntu 22.04 LTS](https://ubuntu.com/download/raspberry-pi)
- Installer [ROS2 humble](https://docs.ros.org/en/humble/Installation.html)
- Installer docker [optionnel]

## Installation de la Stack Robotique | ROS2 🤖

:::warning

L'installation de la stack robotique est nécessaire pour contrôler le MiniPock

:::

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
<TabItem value="standalone" label="Standalone 🖥" default>
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

</TabItem>

<TabItem value="docker" label="Docker 🐳">

```shell
git clone git@github.com:catie-aq/minipock.git
cd minipock
```

En utilisant [`devcontainer`](https://code.visualstudio.com/docs/remote/containers) ouvrez le dossier `minipock` dans Visual Studio Code et exécutez la commande VSCode `Dev Containers: Reopen in Container`.

En utlisant docker, exécutez la commande suivante :

```shell
cd .devcontainer
docker build -t minipock .
```

```shell
cd ..
docker run -it -e DISPLAY=${DISPLAY} -e DEBUG=1 -e ROS_DOMAIN_ID=10 --network=host --privileged -v /dev/dri:/dev/dri -v /dev/shm:/dev/shm -v .:/workspaces/minipock/ minipock /bin/bash
```

Une fois dans le container, exécutez les commandes suivantes :

```shell
cd /workspaces/minipock
source /opt/ros/humble/setup.bash
source /workspaces/minipock/install/setup.bash
colcon build --symlink-install --merge-install
```

</TabItem>
</Tabs>

:::info

Une image docker peut être utilisée pour lancer l’agent Micro-ROS (debug et tests)

Documentation officielle : [https://micro.ros.org/docs/tutorials/core/first_application_rtos/zephyr/](https://micro.ros.org/docs/tutorials/core/first_application_rtos/zephyr/)

```bash
docker run -it --rm --env ROS_DOMAIN_ID=10 -v /dev:/dev --privileged --net=host microros/micro-ros-agent:humble udp4 --port 8888
```

:::

## Flasher le MiniPock 🚀

### Installation de la Stack Applicative | Micro ROS 🪁

:::info

Module officiel µROS : [https://github.com/micro-ROS/micro_ros_zephyr_module.git](https://github.com/micro-ROS/micro_ros_zephyr_module)

:::

L’application de la stack applicative est basée sous Zephyr OS. L’application doit exposer un nœud ROS afin de pourvoir interagir avec un environnement ROS2.

- Installer les [outils Zephyr OS](https://docs.zephyrproject.org/latest/develop/getting_started/index.html)
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

### Installation stack Contrôle moteurs

L’application de contrôle moteur est basée sous Mbed OS.

- Installer les [outils Mbed OS](https://6tron.catie-lab.net/ressources_logicielles/mbed/)
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
