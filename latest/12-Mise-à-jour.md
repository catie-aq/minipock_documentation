---
title: Mise à jour
---

## Mise à jour du système embarqué

Les mises à jour sont disponibles dans les realeases du projet [MiniPock](https://github.com/catie-aq/minipock_zephyr-demo/releases).

### Lancer une mise à jour

Le système vérifie au demarrage si une mise à jour est disponible. Si c'est le cas, la mise à jour est téléchargée et installée automatiquement.

Lancer une mise à jour manuellement :

```
firmware update
```

Afficher la version du firmware :

```
firmware version
```

## API du noeud `FirmwareUpdater`

Le noeud `FirmwareUpdater` gère les mises à jour du firmware pour le dispositif MiniPock. Il expose deux services ROS2 : `TrigUpdate` et `GetChunk`.

### Paramètres

- `namespace` (string, défaut : `"minipock_0"`) : Préfixe utilisé pour les noms des services.
- `method` (string, défaut : `"latest"`) : Méthode de mise à jour. Peut être `"latest"` ou une version spécifique.

### Services

#### `TrigUpdate`

Service permettant de vérifier si une nouvelle version du firmware est disponible et de déclencher une mise à jour.

- **Requête :**
  - `actual_version` (message `Version`) : Version actuelle du firmware.

- **Réponse :**
  - `success` (int) : Code de succès ou d'erreur (voir `TrigUpdateErrorCode`).
  - `new_version_available` (bool) : Indique si une nouvelle version est disponible.
  - `new_version` (message `Version`) : Détails de la nouvelle version (si disponible).
  - `size` (int) : Taille du firmware en octets.

#### `GetChunk`

Service permettant de récupérer des segments du firmware.

- **Requête :**
  - `version` (message `Version`) : Version cible du firmware.
  - `chunk_id` (int) : Identifiant du segment demandé.
  - `chunk_size` (int) : Taille du segment en octets.

- **Réponse :**
  - `success` (int) : Code de succès ou d'erreur (voir `GetChunkErrorCode`).
  - `chunk_id` (int) : Identifiant du segment retourné.
  - `chunk_byte` (byte array) : Données du segment.
  - `chunk_checksum` (int) : Somme de contrôle du segment.

### Codes d'erreur

#### `TrigUpdateErrorCode`

- `SUCCESS` (0) : Opération réussie.
- `PARAMETER_NOT_DECLARED` (1) : Paramètre non déclaré.
- `INVALID_METHOD` (2) : Méthode invalide.
- `GITHUB_FETCH_ERROR` (3) : Erreur lors de la récupération des tags GitHub.
- `NO_BIN_FILE` (4) : Aucun fichier `.bin` trouvé.
- `BIN_DOWNLOAD_ERROR` (5) : Erreur lors du téléchargement du fichier `.bin`.
- `SCHEMA_VALIDATION_FAILED` (6) : Échec de la validation du schéma JSON.

#### `GetChunkErrorCode`

- `SUCCESS` (0) : Opération réussie.
- `VERSION_NOT_FOUND` (1) : Version non trouvée.
- `END_OF_FILE` (2) : Fin du fichier atteinte.

### Protocole de mise à jour

![schema](../img/mise_a_jour.drawio.png)
