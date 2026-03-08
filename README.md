# Documentation Maison

Dépôt centralisé de documentation pour toute la configuration de la maison : réseau, NAS, domotique, électricité, etc.

## Structure

| Dossier | Description | Statut |
|---------|-------------|--------|
| `certificats/` | Certificats SSL et TLS | ✅ En cours |
| `nas/` | Configuration du NAS Synology | ✅ Documenté |
| `reseau/` | Réseau, routeur, switch, Wi-Fi | 🔜 À venir |
| `domotique/` | Home Assistant, objets connectés | 🔜 À venir |

## Guides disponibles

- [Certificat Let's Encrypt sur NAS Synology](certificats/synology-nas/README.md)

## Documentation NAS

- [NAS01 — Synology DS918+](nas/nas01/README.md) — Vue d'ensemble
  - [Réseau](nas/nas01/reseau.md) — Bond, IP, DNS, ports
  - [Stockage](nas/nas01/stockage.md) — Volume, dossiers partagés
  - [Utilisateurs](nas/nas01/utilisateurs.md) — Comptes, groupes, permissions
  - [Services](nas/nas01/services.md) — SMB, FTP, SSH, Plex, Git, etc.
  - [Sécurité](nas/nas01/securite.md) — Pare-feu, TLS, auto-blocage
  - [Notifications](nas/nas01/notifications.md) — Configuration email
