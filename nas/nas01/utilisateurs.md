# NAS01 — Utilisateurs et groupes

## Utilisateurs

| Nom | UID | Description | Email | Statut |
|-----|-----|-------------|-------|--------|
| **admin** | 1024 | Compte système | — | Désactivé |
| **Aryane** | 1029 | Aryane | arystgermain04@gmail.com | Actif |
| **dstgermain** | 1028 | Denis | denis@decizif.com | Actif (admin) |
| **guest** | 1025 | Invité | — | Désactivé |
| **lucas** | 1030 | Lucas | lstgermain@videotron.qc.ca | Actif |
| **marianne** | 1031 | Marianne | mariannesinclair488@gmail.com | Actif |
| **plex** | 1026 | Plex User | — | Actif |
| **sygituser** | 1027 | Utilisateur Git | — | Actif |

> Le compte `admin` par défaut est désactivé (bonne pratique de sécurité). Le compte administrateur principal est `dstgermain`.

## Groupes

| Groupe | Membres |
|--------|---------|
| **administrators** | admin, dstgermain |
| **video** | plex |

> Tous les utilisateurs sont dans le groupe `users` (GID 100) par défaut.

## Privilèges des applications

### dstgermain (admin principal)

Accès à : DSM, File Station, FTP, Surveillance Station, Synology Finder, Rsync, SFTP, AFP, Download Station, SMB, WebDAV

### Groupe administrators

Accès à : Download Station, WebDAV, File Station, Synology Finder, Synology Photos, Surveillance Station, Synology Drive

### Privilèges sur les dossiers partagés

Seul le dossier `surveillance` a des privilèges explicites :

| Utilisateur/Groupe | Privilège |
|--------------------|-----------|
| dstgermain | RW |
| SurveillanceStation | RW |
| administrators | RW |
| admin | RW |

> Les autres dossiers utilisent les ACL POSIX/Windows pour les permissions.

## Politique de mots de passe

| Règle | Valeur |
|-------|--------|
| **Longueur minimale** | 6 caractères |
| **Exclure le nom d'utilisateur** | Oui |
| **Majuscules/minuscules** | Non requis |
| **Caractères numériques** | Non requis |
| **Caractères spéciaux** | Non requis |
| **Expiration** | Désactivée |
| **Mot de passe oublié** | Désactivé |
