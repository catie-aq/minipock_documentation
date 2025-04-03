---
title: Installation
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
git clone -b 2.2.0 git@github.com:catie-aq/minipock.git
cd minipock
```

Exécuter la commande suivante pour démarrer le container docker depuis le dossier `minipock`. Vous pouvez aussi utiliser `devcontainer` de VSCode.

```shell
docker compose run minipock-real # pour le robot réel
docker compose run minipock-simulation # pour la simulation
```

Exécuter les commandes suivantes pour compiler le workspace ROS2

```shell
cd /workspaces/
source /opt/ros/jazzy/setup.bash
source /workspaces/minipock/install/setup.bash
colcon build --merge-install --symlink-install
```

</TabItem>

<TabItem value="standalone" label="Standalone 🖥️">

Prérequis 📦

- Installer [Ubuntu 22.04 LTS](https://ubuntu.com/download/raspberry-pi)
- Installer [ROS2 Jazzy](https://docs.ros.org/en/humble/Installation.html)

Créer un workspace ROS2 et cloner les dépôts MiniPock et micro-ROS

```shell
mkdir -p ~/colcon_ws/src
cd ~/colcon_ws/src
git clone -b 2.2.0 git@github.com:catie-aq/minipock.git
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

- Installer les [outils Zephyr OS](https://docs.zephyrproject.org/latest/develop/getting_started/index.html)
- Initialiser le workspace Zephyr

```bash
west init -m https://github.com/catie-aq/zephyr_minipock --mr v2.2.0 minipock
cd minipock
west update
```

- Configurer les réseaux Wi-Fi

```bash
CONFIG_MICROROS_WIFI_SSID="ssid"
CONFIG_MICROROS_WIFI_PASSWORD="password"
```

:::info

Le SSID et le mot de passe peuvent être configurés avec une commande shell ([documentation](3-Démarrage-rapide.md#configuration-des-paramètres-du-robot)).

:::

```bash

- Compiler l’application

```bash
west build -b zest_core_stm32h753zi app/base-application
```

- Flasher la carte

```bash
west flash
```

### Installation stack Contrôle moteurs

L’application de contrôle moteur est basée sous Mbed OS.

- Installer les [outils Mbed OS](https://6tron.catie-lab.net/ressources_logicielles/mbed/)
- Télécharger le code source

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
