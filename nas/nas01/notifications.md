# NAS01 — Notifications

## Email (SMTP)

| Paramètre | Valeur |
|-----------|--------|
| **Activé** | Oui |
| **Serveur SMTP** | smtp.gmail.com |
| **Port** | 465 |
| **SSL** | Oui |
| **Authentification** | Google OAuth |
| **Compte expéditeur** | thekneestg@gmail.com |
| **Nom expéditeur** | Synology DiskStation |
| **Préfixe sujet** | [10.0.0.105] |
| **Destinataire** | dstgermain@videotron.qc.ca |

> L'adresse IP dans le préfixe du sujet (10.0.0.105) correspond à l'IP du NAS sur le réseau local.

## Push (Mobile)

- **Activé** : Non

## SMS

- **Activé** : Non

## Webhook

- **Configuré** : Non

## Types de notifications

Les notifications sont configurées par canal (desktop, mail, sms, mobile, cms). Les événements critiques (panne disque, crash RAID, surchauffe, etc.) sont envoyés par email. Les événements informatifs (mises à jour, tâches terminées) apparaissent uniquement sur le bureau DSM.
