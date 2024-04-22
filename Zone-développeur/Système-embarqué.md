---
title: Système embarqué
sidebar_position: 6
slug: /6f71a044-b7ee-4e9f-b762-2d7667ff2637
---



## Architecture {#7e03927da8fc45818ec435f2b3b69272}

![](../img/1044571662.png)

## Interface {#cf465c6ecfe1442ca910367aada66ae0}

- La communication entre les nœuds ROS2 et la stack applicative utilise les topics ROS.
- La communication entre la stack applicative et le RBDC utilise les messages protobuf.

```mermaid
flowchart LR
  RO2_nav --WiFi ROS--> µROS_agent
  subgraph Minipock
  subgraph RPI
  µROS_agent
  end
  µROS_agent --UART µROS--> app_µROS
 app_µROS --UART Protobuf--> RBDC
  end
  
```

## Communication µROS - ROS2 {#3a7cbeeb6d0d4894808da1fd514ed1cb}

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

### Liste des topics {#4ccd31d432fc4e44a7702ece040880b1}

| Topic    | Type     |
| -------- | -------- |
| /cmd_vel | Twist    |
| /odom    | odometry |

### Communication micro-ROS ↔RBDC | Protocol Buffer {#fb6e5ec426084f5bae3dbbebe04b5d5c}

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
