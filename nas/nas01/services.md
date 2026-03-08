# NAS01 — Services

## Services de fichiers

### SMB/CIFS

| Paramètre | Valeur |
|-----------|--------|
| **Activé** | Oui |
| **Workgroup** | WORKGROUP |
| **Protocole max** | SMB2 |
| **Protocole min** | NT1 |
| **Symlinks** | Activé |
| **Widelinks** | Désactivé |
| **Log transferts** | Activé (suppression uniquement) |
| **Shadow Copy** | Activé |
| **Multichannel** | Désactivé |
| **NTLMv1** | Désactivé |
| **Server Signing** | Désactivé |

### FTP/FTPS

| Paramètre | Valeur |
|-----------|--------|
| **FTP activé** | Oui |
| **Port** | 21 |
| **SSL/TLS** | Activé |
| **Ports passifs** | 55536 — 55899 |
| **UTF-8** | Activé |
| **Timeout** | 300 secondes |
| **Chroot** | Désactivé |
| **Anonyme** | Désactivé |
| **SFTP** | Désactivé |

### AFP

- **Activé** : Non

### NFS

- **Activé** : Non
- Aucune règle NFS configurée

### WebDAV

- Configuré (profils TLS présents pour synowebdavserver)

## Accès distant

### SSH

| Paramètre | Valeur |
|-----------|--------|
| **Activé** | Oui |
| **Port** | 34522 |
| **Telnet** | Désactivé |

### Rsync / Network Backup

| Paramètre | Valeur |
|-----------|--------|
| **Net Backup** | Désactivé |
| **Rsync SSH port** | 22 |
| **Time Backup** | Activé |

## Services Synology

| Service | Statut |
|---------|--------|
| **Synology Drive** | Installé (port 6690 ouvert dans le firewall) |
| **Synology Photos** | Installé |
| **Surveillance Station** | Installé |
| **Download Station** | Installé |
| **Web Station** | Installé (dossiers web, web_packages) |
| **Plex Media Server** | Installé (utilisateur dédié `plex`) |
| **Git Server** | Installé (utilisateur dédié `sygituser`) |
| **C2 Share** | Configuré (vide) |

## Domaine / LDAP

| Service | Statut |
|---------|--------|
| **Active Directory** | Non joint (WORKGROUP) |
| **LDAP** | Désactivé |
| **SSO Client** | Configuration par défaut |

## SNMP

- **Activé** : Non
