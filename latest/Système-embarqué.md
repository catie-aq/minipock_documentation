---
title: Système embarqué
sidebar_position: 13
---

## Aperçu

Le système embarqué MiniPock est composé de deux parties :
- La stack applicative qui gère la navigation et communique avec la stack de controle moteur. Elle intègre micro-ROS pour la communication avec les nœuds ROS2 et est basée sur Zephyr OS.
- La stack de controle moteur permet déplacer le robot. Elle intègre le RBDC (Robot Base Driver Control) qui permet de demander un déplacement en x, y, theta.

## Architecture

![image1](../img/minipock_architecture_2.1.0.svg)

## Interface

- La communication entre les nœuds ROS2 et la stack applicative utilise les topics ROS.
- La communication entre la stack applicative et le RBDC utilise les messages protobuf.

```mermaid
flowchart LR
  RO2_nav --ROS2 msg--> µROS_agent
  µROS_agent
  µROS_agent --[Wi-Fi] µROS msg --> app_µROS
  subgraph Minipock
  app_µROS --[UART] Protobuf--> RBDC
  end

```

## Communication µROS - ROS2

```mermaid
flowchart LR
subgraph Nav2
BTNavigationServer <--> ControllerServer
BTNavigationServer <--> PlannerServer
ControllerServer --> PlannerServer

end
ControllerServer --> VelocitySmoother
VelocitySmoother --> CollisionMonitor
CollisionMonitor --> RobotBase
RobotBase --/cmd_vel Twist--> Zephyr_µROS
Zephyr_µROS --/odom Odometry--> ControllerServer
RPi --/scan LaserScan--> PlannerServer
RPi --/tf TfMsg-->PlannerServer
```

### Liste des topics

| Topic        | Type        |
| ------------ | ----------- |
| /namespace/cmd_vel  | Twist       |
| /namespace/odom_raw | PoseStamped |
| /namespace/scan_raw | LaserScan   |

### Communication micro-ROS ↔RBDC | Protocol Buffer

```protobuf
syntax = "proto3";

message cmd_vel {
  float linear_x = 1;
  float linear_y = 2;
  float linear_z = 3;
  float angular_x = 4;
  float angular_y = 5;
  float angular_z = 6;
}

message odom {
  float x = 1;
  float y = 2;
  float theta = 3;
}
```
