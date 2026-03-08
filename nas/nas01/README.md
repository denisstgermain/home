# NAS01 — Synology DS918+

Documentation de la configuration du NAS principal, extraite de l'export DSM du 2026-03-08.

## Informations générales

| Paramètre | Valeur |
|-----------|--------|
| **Nom** | NAS01 |
| **Modèle** | Synology DS918+ (apollolake) |
| **OS** | DSM 7.2 (build 72806) |
| **Fuseau horaire** | Bogota (America/Bogota) |
| **Serveur NTP** | time.google.com (serveur NTP local activé) |
| **Langue** | Défaut (anglais, mails en anglais) |
| **Format date** | Y-m-d, H:i |

## Sections

| Document | Description |
|----------|-------------|
| [Réseau](reseau.md) | Bond, IP, DNS, passerelle, ports |
| [Stockage](stockage.md) | Volume, dossiers partagés |
| [Utilisateurs](utilisateurs.md) | Comptes, groupes, permissions |
| [Services](services.md) | SMB, FTP, SSH, services actifs |
| [Sécurité](securite.md) | Pare-feu, auto-blocage, TLS, mots de passe |
| [Notifications](notifications.md) | Configuration email SMTP |

## Mises à jour DSM

- **Mode** : Notification uniquement (pas d'auto-install)
- **Vérification** : Mercredi et samedi à 6h25
- **Smart Nano** : Activé
