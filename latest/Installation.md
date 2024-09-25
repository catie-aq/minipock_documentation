---
title: Installation
sidebar_position: 3
---

## Installation PC

:::warning

L'installation de la stack robotique est nécessaire pour contrôler le MiniPock

:::

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
<TabItem value="docker" label="Docker 🐳" default>

```shell
git clone -b 2.1.0 git@github.com:catie-aq/minipock.git
cd minipock
```

Exécutez la commande suivante pour démarrer le container docker depuis le dossier `minipock`

```shell
docker compose run minipock-real # pour le robot réel
docker compose run minipock-simulation # pour la simulation
```

Pour compiler le workspace ROS2, exécutez les commandes suivantes

```shell
cd /workspaces/minipock
source /opt/ros/jazzy/setup.bash
source /workspaces/minipock/install/setup.bash
colcon build --merge-install
```

</TabItem>

<TabItem value="standalone" label="Standalone 🖥️">

Prérequis 📦

- Installer [Ubuntu 22.04 LTS](https://ubuntu.com/download/raspberry-pi)
- Installer [ROS2 Jazzy](https://docs.ros.org/en/humble/Installation.html)
  
Créér un workspace ROS2 et cloner les dépôts MiniPock

```shell
mkdir -p ~/colcon_ws/src
cd ~/colcon_ws/src
git clone -b 2.1.0 git@github.com:catie-aq/minipock.git
git clone -b jazzy https://github.com/micro-ROS/micro_ros_setup.git
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

</Tabs>

## Installation MiniPock 🚀

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
