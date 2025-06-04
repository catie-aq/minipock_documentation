# Endpoints HTTP

## Endpoints statiques

- **GET /**
  - Sert le fichier HTML compressé (`index.html.gz`).

- **GET /main.js**
  - Sert le fichier JavaScript compressé (`main.js.gz`).

- **GET /style.css**
  - Sert le fichier CSS compressé (`style.css.gz`).

## Endpoints dynamiques

- **GET /uptime**
  - Retourne le temps de fonctionnement du système en millisecondes.

- **GET /version**
  - Retourne la version actuelle sous forme JSON.
  - Exemple : `{"version":"1.0.0"}`

- **GET /ssid**
  - Retourne le SSID WiFi actuel sous forme JSON.
  - Exemple : `{"ssid":"MyNetwork"}`

- **POST /update_network**
  - Met à jour les paramètres réseau (SSID et mot de passe) via JSON.

- **POST /update_ros_settings**
  - Met à jour les paramètres ROS (namespace et IP de l'agent) via JSON.

- **GET /ip**
  - Retourne l'adresse IP actuelle sous forme JSON.
  - Exemple : `{"ip_address":"192.168.1.1"}`

- **GET /namespace**
  - Retourne le namespace ROS actuel sous forme JSON.
  - Exemple : `{"namespace":"my_namespace"}`

- **GET /domain_id**
  - Retourne l'ID de domaine ROS configuré sous forme JSON.
  - Exemple : `{"domain_id":"42"}`

- **GET /micro_ros_status**
  - Retourne le statut actuel de micro-ROS sous forme JSON.
  - Exemple : `{"status":"active"}`

- **POST /estop**
  - Active ou désactive l'arrêt d'urgence via JSON.
  - Exemple : `{"active":true}`

- **POST /factory_reset**
  - Réinitialise les paramètres du système aux valeurs d'usine.

- **POST /restart_system**
  - Redémarre le système.

- **GET /agent_ip**
  - Retourne l'adresse IP de l'agent micro-ROS sous forme JSON.
  - Exemple : `{"agent_ip":"192.168.1.100"}`