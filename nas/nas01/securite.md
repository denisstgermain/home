# NAS01 — Sécurité

## Pare-feu (Firewall)

- **Activé** : Oui
- **Profil actif** : default

### Règles

| # | Direction | Ports | Protocole | Source | Action |
|---|-----------|-------|-----------|--------|--------|
| 1 | Entrée | 6690 | TCP | Toutes | Autoriser |
| — | Politique par défaut | Tous | Tous | Toutes | Refuser |

> Le port 6690 est utilisé par **Synology Drive**.
> La politique par défaut est de **refuser** tout le trafic non explicitement autorisé (adapterPolicy = 2).

## Auto-blocage

| Paramètre | Valeur |
|-----------|--------|
| **Tentatives max** | 10 |
| **Période** | 5 minutes |
| **Expiration du blocage** | 1 jour |

## Protection DoS

Non configurée.

## Profil TLS

### DSM (nginx)

```
ssl_protocols               TLSv1.2 TLSv1.3;
ssl_ciphers                 ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:
                            ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:
                            ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305;
ssl_dhparam                 /usr/syno/etc/ssl/dh2048.pem;
```

- **Niveau TLS par défaut** : 2 (Modern compatibility)
- **DSM** : Niveau 0 (personnalisé — voir ci-dessus)
- **FTPS** : Niveau 0

> Bonne configuration : TLS 1.0/1.1 désactivés, uniquement des ciphers AEAD modernes.

## Protection DSM

| Paramètre | Valeur |
|-----------|--------|
| **En-tête CSP** | Activé |
| **Protection CSRF** | Activée |
| **Nettoyage session au redémarrage** | Oui |
| **Vérification IP session** | Oui |
| **Timeout session** | 15 minutes |

### Embed / iFrame

- **Blocage iFrame** : Activé
- **Whitelist** : gofile.me/, find.synology.com/

## Observations et recommandations

### Points positifs
- Compte admin par défaut désactivé
- TLS 1.2+ uniquement avec ciphers modernes
- Pare-feu activé avec politique de refus par défaut
- Port SSH changé (34522 au lieu de 22)
- Auto-blocage configuré

### Points à améliorer
- Le protocole SMB minimum est NT1 (SMBv1) — envisager de passer à SMB2 minimum si tous les clients le supportent
- Pas de redirection HTTP → HTTPS
- HSTS non activé
- La politique de mots de passe pourrait être renforcée (majuscules, chiffres, caractères spéciaux)
- FTP activé — envisager SFTP uniquement si possible
- NTLMv1 désactivé (bien), mais SMBv1 encore permis
