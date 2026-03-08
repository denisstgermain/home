# Certificat Wildcard Let's Encrypt — fstgermain.com

Certificat SSL wildcard `*.fstgermain.com` + `fstgermain.com` généré via acme.sh et Cloudflare DNS-01.

---

## Certificat actif

| Paramètre | Valeur |
|-----------|--------|
| **Domaines** | `fstgermain.com` + `*.fstgermain.com` |
| **Émetteur** | Let's Encrypt (E8) |
| **Type de clé** | ECC (ECDSA P-256) |
| **Validité** | 90 jours (renouvellement auto) |
| **Première émission** | 2026-03-08 |
| **Expiration** | 2026-06-06 |
| **Validation** | DNS-01 via Cloudflare API |

## Fichiers du certificat

Les fichiers sont stockés sur la machine Windows de génération :

```
C:\Users\Denis\.acme.sh\fstgermain.com_ecc\
├── fstgermain.com.cer      ← Certificat serveur
├── fstgermain.com.key      ← Clé privée
├── ca.cer                  ← Certificat intermédiaire (CA)
├── fullchain.cer           ← Certificat + chaîne complète (pour la plupart des services)
└── fstgermain.com.conf     ← Configuration acme.sh (ne pas modifier)
```

---

## Génération et renouvellement

### Prérequis (déjà en place)

- **acme.sh** installé dans `C:\Users\Denis\.acme.sh\`
- **Cloudflare API Token** : configuré dans le projet `D:\GithubRepo\cloudflare\`
- **Zone ID** : `4564124ff5baebc49dbcbf896a10e763`
- Un **Windows Scheduler Task** a été créé pour le renouvellement automatique

### Commande de génération / renouvellement manuel

```bash
export CF_Token="<token_cloudflare>"
export CF_Zone_ID="4564124ff5baebc49dbcbf896a10e763"

~/.acme.sh/acme.sh --issue --dns dns_cf \
  -d fstgermain.com \
  -d "*.fstgermain.com" \
  --server letsencrypt --force
```

### Renouvellement automatique

acme.sh a installé une tâche planifiée Windows qui renouvelle automatiquement le certificat avant expiration. Vérifier :

```bash
# Voir la config
cat ~/.acme.sh/fstgermain.com_ecc/fstgermain.com.conf

# Renouvellement manuel si besoin
~/.acme.sh/acme.sh --renew -d fstgermain.com -d "*.fstgermain.com" --force
```

---

## Déploiement sur NAS Synology (NAS01)

### Option A : Import manuel via DSM

1. Copier les 3 fichiers nécessaires depuis `C:\Users\Denis\.acme.sh\fstgermain.com_ecc\` :
   - `fstgermain.com.key` (clé privée)
   - `fstgermain.com.cer` (certificat)
   - `ca.cer` (certificat intermédiaire)
2. Dans DSM : **Panneau de configuration → Sécurité → Certificat**
3. **Ajouter → Importer un certificat**
4. Remplir les champs :
   - **Clé privée** : `fstgermain.com.key`
   - **Certificat** : `fstgermain.com.cer`
   - **Certificat intermédiaire** : `ca.cer`
5. Cocher **Définir comme certificat par défaut** si désiré
6. Cliquer **OK**

### Option B : Déploiement automatique via acme.sh (deploy hook)

> **Note** : Le 2FA est activé sur le compte `dstgermain`. Il faut configurer `SYNO_DEVICE_NAME` et `SYNO_DEVICE_ID` pour que le deploy hook fonctionne.

```bash
# Configuration initiale (une seule fois)
export SYNO_USERNAME='dstgermain'
export SYNO_PASSWORD='<mot_de_passe>'
export SYNO_SCHEME='https'
export SYNO_HOSTNAME='10.0.0.105'
export SYNO_PORT='5001'
export SYNO_DEVICE_NAME='CertBot'
export SYNO_DEVICE_ID='<device_id>'   # Obtenu lors du premier login 2FA

# Déployer
~/.acme.sh/acme.sh --deploy -d fstgermain.com --deploy-hook synology_dsm
```

Pour obtenir le `SYNO_DEVICE_ID`, voir la [doc du deploy hook Synology](https://github.com/acmesh-official/acme.sh/wiki/deployhooks#20-deploy-the-cert-into-synology-dsm).

### Après le déploiement

1. **Panneau de configuration → Sécurité → Certificat → Paramètres**
2. Assigner le certificat `fstgermain.com` à chaque service :
   - DSM Desktop Service
   - Web Station
   - Synology Drive
   - Tout autre service HTTPS
3. Vérifier : `https://drive.fstgermain.com:5001` → cadenas valide

---

## Déploiement sur d'autres services

Le certificat wildcard couvre **tous les sous-domaines** de fstgermain.com. Il peut être installé sur n'importe quel service :

| Service | Fichiers nécessaires |
|---------|---------------------|
| Nginx / Apache | `fullchain.cer` + `fstgermain.com.key` |
| NAS Synology | `fstgermain.com.cer` + `fstgermain.com.key` + `ca.cer` |
| Home Assistant | `fullchain.cer` + `fstgermain.com.key` |
| Autre | Varie — généralement fullchain + key |

---

## Dépannage

| Problème | Solution |
|----------|----------|
| `Cannot find DNS API hook for: dns_cf` | Les plugins dnsapi manquent. Cloner le repo acme.sh et copier `dnsapi/` dans `~/.acme.sh/` |
| Échec validation DNS-01 | Vérifier le token Cloudflare et le Zone ID. Tester : `curl -s -H "Authorization: Bearer $CF_Token" "https://api.cloudflare.com/client/v4/zones/$CF_Zone_ID"` |
| Certificat expiré | `~/.acme.sh/acme.sh --renew -d fstgermain.com -d "*.fstgermain.com" --force` |
| Erreur 2FA sur deploy hook Synology | Configurer `SYNO_DEVICE_NAME` + `SYNO_DEVICE_ID` |
| Renouvellement Windows échoue | Vérifier la tâche planifiée dans le Planificateur de tâches Windows |
