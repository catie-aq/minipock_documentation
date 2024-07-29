---
title: Électronique
sidebar_position: 14
---

## Aperçu

L'electronique de la plateforme 6TRON est basée sur les cartes 6TRON et la stack applicative. Elle est composée de deux parties :
- La stack applicative qui gère la navigation et la communication avec la stack moteur.
- La stack moteur qui gère les moteurs.

![Architecture](../img/general_architecture.png)

## Stack applicative

Cartes 6TRON :
- [Zest_Carrier_Extension](https://6tron.io/zest/zest_carrier_extension_1_0_0)
- [Zest_Core_STM32L4A6RG](https://6tron.io/zest_core/zest_core_stm32l4a6rg_3_1_0)
- [Zest_Test_Prototyping](https://6tron.io/zest/zest_test_prototyping_1_0_0)

### LiDAR

#### Caractéristiques

Référence : LD19

#### Connection

| LiDAR | 6TRON   |
| ----- | ------- |
| TX    | DIO12   |
| PWM   | GND     |

### RBDC interface

La stack applicative communique avec le RBDC via une interface UART. Le protocol de communication est basé sur des messages protobuf.

```mermaid
flowchart LR
  app_µROS --UART Protobuf--> RBDC
```
### Connection

| RBDC | 6TRON   |
| ---- | ------- |
| TX   | UART_RX |
| RX   | UART_TX |

## Stack moteur

Cartes 6TRON :
- [Zest_Carrier_Extension](https://6tron.io/zest/zest_carrier_extension_1_0_0)
- [Zest_Core_STM32G474VET](https://6tron.io/zest/zest_core_stm32g474vet_1_0_0)
- [Zest_Actuator_HalfBridges](https://6tron.io/zest/zest_actuator_halfbridges_1_0_0)
- [Zest_Test_Prototyping](https://6tron.io/zest/zest_test_prototyping_1_0_0)

![image2](../img/574645014.jpg)

![image3](../img/553523925.png)
