# NAS01 — Stockage

## Volume

| Paramètre | Valeur |
|-----------|--------|
| **Volume** | volume1 |
| **Point de montage** | /volume1 |
| **Système de fichiers** | Btrfs |
| **Emplacement** | Pool 1 |

## Dossiers partagés

| Dossier | Chemin | Description | Corbeille | Chiffré |
|---------|--------|-------------|-----------|---------|
| **Backup** | /volume1/Backup | — | Non | Non |
| **Denis** | /volume1/Denis | — | Oui | Non |
| **Famille** | /volume1/Famille | — | Oui | Non |
| **Git** | /volume1/Git | Source Control | Non | Non |
| **homes** | /volume1/homes | Dossiers personnels | Non | Non |
| **Media** | /volume1/Media | — | Non | Non |
| **nordia** | /volume1/nordia | nordi | Non | Non |
| **photo** | /volume1/photo | Dossier système | Non | Non |
| **Plex** | /volume1/Plex | Plex metadata storage | Non | Non |
| **PlexMediaServer** | /volume1/PlexMediaServer | — | Non | Non |
| **Scan** | /volume1/Scan | Scan | Oui | Non |
| **Share** | /volume1/Share | — | Oui | Non |
| **Sources** | /volume1/Sources | — | Non | Non |
| **surveillance** | /volume1/surveillance | Dossier système | Non | Non |
| **Temp** | /volume1/Temp | — | Non | Non |
| **web** | /volume1/web | Dossier système | Non | Non |
| **web_packages** | /volume1/web_packages | — | Non | Non |

## Service Home

- **Activé** : Oui
- **Volume** : /volume1/homes
- **Utilisateurs LDAP** : Non inclus
- **Utilisateurs domaine** : Non inclus
- **Corbeille** : Désactivée

## Indexation média

- **Dossier indexé** : /photo (type : photo)
- **Qualité miniatures** : Normale
- **Planification conversion** : Toujours active

## Quotas

Aucun quota configuré (ni utilisateur, ni groupe).
