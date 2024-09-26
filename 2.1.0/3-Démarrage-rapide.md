---
title: Démarrage rapide
---

:::warning

Ce guide suppose que vous avez un (ou plusieurs) MiniPock flashé prêt à l'emploi

:::

Pour communiquer avec le MiniPock assurez vous d'être sur le même `ROS_DOMAIN_ID` que le MiniPock (par défaut `10`) et sur le même réseau que le MiniPock

## Configuration de la flotte

La configuration de la flotte se fait dans le fichier `minipock/minipocks.yaml`

```yaml
namespace: minipock_ # pattern de nommage des namespaces minipock_0, minipock_1, ...
bringup: false # true en cas de robot réel
use_sim_time: true # false en cas de robot réel
fleet:
  "0": # nom du robot
    mode: differential # mode de contrôle differential ou holonomic
    position: null # position initiale du robot null pour aléatoire
```

Lorsque plusieurs robots sont spécifiés dans le fichier de configuration, les différents robots sont lancés avec le namespace spécifié dans le fichier de configuration et un numéro incrémenté à la fin du namespace.

:::warning

Dans le cas des robots réels chaque robot possède un namespace et un numéro unique, il faut donc avoir un fichier cohérent avec la configuration des robots réels

:::

## Bringup

:::danger

Ce noeud est nécessaire **uniquement** pour manipuler le robot réel. Il permet la communication avec le robot réel.

:::

:::info

Il est automatiquement lancé par les différentes stack si le paramètre `bringup` est à `true`

:::

```shell
ros2 launch minipock_bringup bringup.launch.py
```

## Téléopération

Lancez ensuite le noeud de téléopération

```bash
ros2 run minipock_teleop teleop_fps --ros-args -p namespace:=robot_namespace/
```

Si aucun namespace n'est spécifié ou qu'il est inéxistant, le premier topic comportant `cmd_vel` sera utilisé.

Vous pouvez ensuite contrôler le robot avec les touches `zqsd` pour avancer, tourner à gauche, reculer et tourner à droite et `b` pour activer le boost.
