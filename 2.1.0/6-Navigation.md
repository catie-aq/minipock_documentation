---
title: Navigation
---



La navigation consiste à déplacer le robot d'un endroit à la destination spécifiée dans un environnement donné. Pour ce faire, une carte contenant des informations géométriques sur les meubles, les objets et les murs de l'environnement donné est nécessaire. Comme décrit dans la section SLAM précédente, la carte a été créée avec les informations de distance obtenues par le capteur et les informations de pose du robot lui-même.

La navigation permet à un robot de se déplacer de la position actuelle à la position cible désignée sur la carte en utilisant la carte, l'encodeur du robot, le capteur IMU et le capteur de distance. La procédure d'exécution de cette tâche est la suivante.

## Lancement de la navigation

```shell
ros2 launch minipock_navigation2 navigation2.launch.py
```

:::info

Les informations sur le nombre de robots, leurs types, le lancement du bringup sont contenus dans le fichier de configuration `minipock/minipocks.yaml`

:::

La `map` utilisée est le fichier `map.yaml` dans `minipock_navigation2/map/map.yaml`

## Estimer la position initiale

- Cliquez sur le bouton 2D Pose Estimate dans le menu RViz2.
- Cliquez sur la carte où se trouve le robot et faites glisser la flèche verte vers la direction à laquelle le robot fait face.

## Donner un ordre de navigation

- Cliquez sur le bouton Navigation2 Goal dans le menu RViz2.
- Cliquez sur la carte pour définir la destination du robot et faites glisser la flèche verte vers la direction vers laquelle le robot sera orienté.
  - Cette flèche verte est un marqueur qui permet de spécifier la destination du robot.
  - La racine de la flèche correspond aux coordonnées x, y de la destination, et l'angle θ est déterminé par l'orientation de la flèche.
  - Dès que x, y, θ sont définis, TurtleBot3 commence immédiatement à se déplacer vers la destination.

![image](../img/1887772889.png)

## Paramétrage

Les paramètres de navigation sont paramétrables dans le fichier [`minipock.yaml`](https://github.com/catie-aq/minipock_navigation/blob/main/minipock_navigation2/param/minipock.yaml).

## API Documentation

### `/namespace/amcl`

Responsable de la localisation adaptative Monte Carlo (AMCL).

- **Subscribers:**
  - `/map` - `nav_msgs/msg/OccupancyGrid` : Carte d'occupation
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/initialpose` - `geometry_msgs/msg/PoseWithCovarianceStamped` : Pose initiale
  - `/namespace/scan` - `sensor_msgs/msg/LaserScan` : Scans du lidar
- **Publishers:**
  - `/namespace/amcl/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition
  - `/namespace/amcl_pose` - `geometry_msgs/msg/PoseWithCovarianceStamped` : Pose estimée
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/particle_cloud` - `nav2_msgs/msg/ParticleCloud` : Nuage de particules
  - `/tf` - `tf2_msgs/msg/TFMessage` : Transformations entre les différents repères

### `/namespace/behavior_server`

Responsable de la gestion des comportements du robot.

- **Subscribers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/local_costmap/costmap_raw` - `nav2_msgs/msg/Costmap` : Carte de coût locale brute
  - `/namespace/local_costmap/costmap_raw_updates` - `nav2_msgs/msg/CostmapUpdate` : Mises à jour de la carte de coût locale brute
  - `/namespace/local_costmap/published_footprint` - `geometry_msgs/msg/PolygonStamped` : Empreinte publiée
- **Publishers:**
  - `/namespace/behavior_server/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/cmd_vel` - `geometry_msgs/msg/Twist` : Commande de vitesse

### `/namespace/collision_monitor`

Responsable de la surveillance des collisions.

- **Subscribers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/cmd_vel_smoothed` - `geometry_msgs/msg/Twist` : Commande de vitesse lissée
  - `/namespace/local_costmap/published_footprint` - `geometry_msgs/msg/PolygonStamped` : Empreinte publiée
  - `/namespace/namespace/scan` - `sensor_msgs/msg/LaserScan` : Scans du lidar
- **Publishers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/cmd_vel` - `geometry_msgs/msg/Twist` : Commande de vitesse
  - `/namespace/collision_monitor/collision_points_marker` - `visualization_msgs/msg/MarkerArray` : Marqueurs des points de collision
  - `/namespace/collision_monitor/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition
  - `/namespace/collision_monitor_state` - `nav2_msgs/msg/CollisionMonitorState` : État du moniteur de collision

### `/namespace/controller_server`

Responsable de la gestion du serveur de contrôleur.

- **Subscribers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/odom` - `nav_msgs/msg/Odometry` : Odométrie du robot
  - `/namespace/speed_limit` - `nav2_msgs/msg/SpeedLimit` : Limite de vitesse
- **Publishers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/cmd_vel` - `geometry_msgs/msg/Twist` : Commande de vitesse
  - `/namespace/controller_server/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition
  - `/namespace/cost_cloud` - `sensor_msgs/msg/PointCloud2` : Nuage de points de coût
  - `/namespace/evaluation` - `dwb_msgs/msg/LocalPlanEvaluation` : Évaluation du plan local
  - `/namespace/local_plan` - `nav_msgs/msg/Path` : Plan local
  - `/namespace/marker` - `visualization_msgs/msg/MarkerArray` : Marqueurs de visualisation
  - `/namespace/received_global_plan` - `nav_msgs/msg/Path` : Plan global reçu
  - `/namespace/transformed_global_plan` - `nav_msgs/msg/Path` : Plan global transformé

### `/namespace/global_costmap/global_costmap`

Responsable de la gestion de la carte de coût globale.

- **Subscribers:**
  - `/map` - `nav_msgs/msg/OccupancyGrid` : Carte d'occupation
  - `/namespace/global_costmap/footprint` - `geometry_msgs/msg/Polygon` : Empreinte du robot
  - `/namespace/scan` - `sensor_msgs/msg/LaserScan` : Scans du lidar
- **Publishers:**
  - `/namespace/global_costmap/costmap` - `nav_msgs/msg/OccupancyGrid` : Carte de coût
  - `/namespace/global_costmap/costmap_raw` - `nav2_msgs/msg/Costmap` : Carte de coût brute
  - `/namespace/global_costmap/costmap_raw_updates` - `nav2_msgs/msg/CostmapUpdate` : Mises à jour de la carte de coût brute
  - `/namespace/global_costmap/costmap_updates` - `map_msgs/msg/OccupancyGridUpdate` : Mises à jour de la carte de coût
  - `/namespace/global_costmap/global_costmap/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition
  - `/namespace/global_costmap/obstacle_layer` - `nav_msgs/msg/OccupancyGrid` : Couche d'obstacles
  - `/namespace/global_costmap/obstacle_layer_raw` - `nav2_msgs/msg/Costmap` : Couche d'obstacles brute
  - `/namespace/global_costmap/obstacle_layer_raw_updates` - `nav2_msgs/msg/CostmapUpdate` : Mises à jour de la couche d'obstacles brute
  - `/namespace/global_costmap/obstacle_layer_updates` - `map_msgs/msg/OccupancyGridUpdate` : Mises à jour de la couche d'obstacles
  - `/namespace/global_costmap/published_footprint` - `geometry_msgs/msg/PolygonStamped` : Empreinte publiée
  - `/namespace/global_costmap/static_layer` - `nav_msgs/msg/OccupancyGrid` : Couche statique
  - `/namespace/global_costmap/static_layer_raw` - `nav2_msgs/msg/Costmap` : Couche statique brute
  - `/namespace/global_costmap/static_layer_raw_updates` - `nav2_msgs/msg/CostmapUpdate` : Mises à jour de la couche statique brute
  - `/namespace/global_costmap/static_layer_updates` - `map_msgs/msg/OccupancyGridUpdate` : Mises à jour de la couche statique
  - `/parameter_events` - `rcl_interfaces/msg/ParameterEvent` : Événements des paramètres
  - `/rosout` - `rcl_interfaces/msg/Log` : Messages de journalisation

### `/namespace/local_costmap/local_costmap`

Responsable de la gestion de la carte de coût locale.

- **Subscribers:**
  - `/namespace/local_costmap/footprint` - `geometry_msgs/msg/Polygon` : Empreinte du robot
  - `/namespace/scan` - `sensor_msgs/msg/LaserScan` : Scans du lidar
- **Publishers:**
  - `/namespace/local_costmap/costmap` - `nav_msgs/msg/OccupancyGrid` : Carte de coût
  - `/namespace/local_costmap/costmap_raw` - `nav2_msgs/msg/Costmap` : Carte de coût brute
  - `/namespace/local_costmap/costmap_raw_updates` - `nav2_msgs/msg/CostmapUpdate` : Mises à jour de la carte de coût brute
  - `/namespace/local_costmap/costmap_updates` - `map_msgs/msg/OccupancyGridUpdate` : Mises à jour de la carte de coût
  - `/namespace/local_costmap/local_costmap/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition
  - `/namespace/local_costmap/obstacle_layer` - `nav_msgs/msg/OccupancyGrid` : Couche d'obstacles
  - `/namespace/local_costmap/obstacle_layer_raw` - `nav2_msgs/msg/Costmap` : Couche d'obstacles brute
  - `/namespace/local_costmap/obstacle_layer_raw_updates` - `nav2_msgs/msg/CostmapUpdate` : Mises à jour de la couche d'obstacles brute
  - `/namespace/local_costmap/obstacle_layer_updates` - `map_msgs/msg/OccupancyGridUpdate` : Mises à jour de la couche d'obstacles
  - `/namespace/local_costmap/published_footprint` - `geometry_msgs/msg/PolygonStamped` : Empreinte publiée

### `/namespace/planner_server`

Responsable de la gestion du serveur de planification.

- **Subscribers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
- **Publishers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/plan` - `nav_msgs/msg/Path` : Plan de navigation
  - `/namespace/planner_server/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition

### `/namespace/smoother_server`

Responsable de la gestion du serveur de lissage de trajectoire.

- **Subscribers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/global_costmap/costmap_raw` - `nav2_msgs/msg/Costmap` : Carte de coût globale brute
  - `/namespace/global_costmap/costmap_raw_updates` - `nav2_msgs/msg/CostmapUpdate` : Mises à jour de la carte de coût globale brute
  - `/namespace/global_costmap/published_footprint` - `geometry_msgs/msg/PolygonStamped` : Empreinte publiée
- **Publishers:**
  - `/namespace/bond` - `bond/msg/Status` : Statut de la liaison
  - `/namespace/plan_smoothed` - `nav_msgs/msg/Path` : Trajectoire lissée
  - `/namespace/smoother_server/transition_event` - `lifecycle_msgs/msg/TransitionEvent` : Événements de transition
