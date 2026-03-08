# NAS01 — Réseau

## Interface réseau

Le NAS utilise un **bond** (agrégation de liens) sur les deux ports Ethernet.

| Paramètre | Valeur |
|-----------|--------|
| **Interface** | bond0 (eth0 + eth1) |
| **Mode** | 6 — Adaptive Load Balancing |
| **DHCP** | Oui |
| **MTU** | 1500 (eth0 et eth1) |

### Passerelle et DNS

| Paramètre | Valeur |
|-----------|--------|
| **Passerelle IPv4** | 10.0.0.1 |
| **Passerelle IPv6** | fe80::217:10ff:fe8e:361b |
| **DNS** | 1.0.0.1 (Cloudflare) |
| **DNS DHCP** | 10.0.0.1 (depuis le routeur) |

### Options réseau

- **Détection conflit IP** : Activée
- **IPv4 prioritaire** : Non
- **Multi-gateway** : Non
- **Domaine DHCP** : Utilisé
- **ARP ignore** : Activé
- **Proxy** : Désactivé

## Ports d'accès DSM

| Service | Port |
|---------|------|
| **DSM HTTP** | 5000 |
| **DSM HTTPS** | 5001 |
| **Redirection HTTPS** | Non |
| **HSTS** | Non |
| **HTTP/2** | Oui |

## Accès distant

| Service | Statut |
|---------|--------|
| **QuickConnect** | Désactivé |
| **DDNS** | Non configuré |
| **UPnP** | Activé |
| **Reverse Proxy** | Aucune règle |

## Découverte de services

- **SSDP** : Activé
- **WS-Transfer** : Activé
- **Avahi/Bonjour** : Activé
- **Bonjour Printer** : Désactivé
- **Time Machine (AFP)** : Désactivé
- **Time Machine (SMB)** : Désactivé

## Routes statiques

Aucune route statique configurée.
