# Certificat Let's Encrypt — NAS Synology

Guide pour obtenir et configurer un certificat SSL Let's Encrypt sur un NAS Synology (DSM 7+).

---

## Prérequis

- **Nom de domaine** configuré et pointant vers le NAS (A record ou DDNS Synology/autre)
- **Accès admin** au DSM
- **Port 80 accessible** depuis Internet (pour la méthode DSM / HTTP-01), ou accès à l'API DNS de votre registrar (pour la méthode DNS-01 via acme.sh)

---

## Méthode 1 : Via l'interface DSM (la plus simple)

Convient si le port 80 est ouvert et redirigé vers le NAS.

### Étapes

1. Se connecter au DSM en tant qu'administrateur
2. Aller dans **Panneau de configuration → Sécurité → Certificat**
3. Cliquer sur **Ajouter**
4. Sélectionner **Ajouter un nouveau certificat** → Suivant
5. Sélectionner **Obtenir un certificat auprès de Let's Encrypt** → Suivant
6. Remplir les champs :
   - **Nom de domaine** : `votre-domaine.com` (le domaine principal)
   - **E-mail** : votre adresse e-mail (notifications d'expiration)
   - **Autre nom de l'objet (SAN)** : domaines supplémentaires séparés par `;` (optionnel)
7. Cliquer sur **Terminé**

### Renouvellement

DSM renouvelle automatiquement le certificat avant son expiration (tous les 90 jours). Aucune action requise.

---

## Méthode 2 : Via acme.sh en SSH (plus flexible)

Convient si vous ne pouvez pas ouvrir le port 80, ou si vous voulez plus de contrôle. Utilise le challenge **DNS-01** : aucun port à ouvrir.

### 1. Activer SSH sur le NAS

- **Panneau de configuration → Terminal & SNMP → Terminal**
- Cocher **Activer le service SSH**
- Se connecter en SSH : `ssh admin@IP_DU_NAS`

### 2. Installer acme.sh

```bash
# Se connecter en root
sudo -i

# Installer acme.sh
wget -O - https://get.acme.sh | sh -s email=votre@email.com

# Recharger le profil
source ~/.bashrc
```

### 3. Configurer l'API DNS de votre registrar

Chaque registrar a ses propres variables d'environnement. Exemples :

**OVH :**
```bash
export OVH_END_POINT='ovh-eu'
export OVH_AK='votre_application_key'
export OVH_AS='votre_application_secret'
export OVH_CK='votre_consumer_key'
```

**Cloudflare :**
```bash
export CF_Token='votre_api_token'
export CF_Zone_ID='votre_zone_id'
```

> Consultez la [liste complète des DNS API supportés par acme.sh](https://github.com/acmesh-official/acme.sh/wiki/dnsapi).

### 4. Émettre le certificat

```bash
# Exemple avec OVH
~/.acme.sh/acme.sh --issue --dns dns_ovh -d votre-domaine.com -d *.votre-domaine.com

# Exemple avec Cloudflare
~/.acme.sh/acme.sh --issue --dns dns_cf -d votre-domaine.com -d *.votre-domaine.com
```

### 5. Déployer le certificat sur DSM

acme.sh inclut un script de déploiement pour Synology DSM :

```bash
# Configurer les identifiants DSM (une seule fois)
export SYNO_USERNAME='admin'
export SYNO_PASSWORD='votre_mot_de_passe'
export SYNO_SCHEME='https'
export SYNO_HOSTNAME='localhost'
export SYNO_PORT='5001'

# Déployer
~/.acme.sh/acme.sh --deploy -d votre-domaine.com --deploy-hook synology_dsm
```

> **Note :** Si l'authentification à deux facteurs (2FA) est activée sur le compte admin, utilisez `SYNO_DEVICE_NAME` et `SYNO_DEVICE_ID` pour contourner le 2FA. Consultez la [doc du deploy hook](https://github.com/acmesh-official/acme.sh/wiki/deployhooks#20-deploy-the-cert-into-synology-dsm).

### 6. Renouvellement automatique

acme.sh installe automatiquement une entrée cron pour le renouvellement. Vérifier :

```bash
crontab -l
```

Sur Synology, le cron peut être réinitialisé après une mise à jour DSM. Pour plus de fiabilité, créer une **tâche planifiée** dans DSM :

1. **Panneau de configuration → Planificateur de tâches → Créer → Tâche planifiée → Script défini par l'utilisateur**
2. **Planification** : une fois par jour (ou par semaine)
3. **Script** :
   ```bash
   /root/.acme.sh/acme.sh --cron --home /root/.acme.sh
   ```
4. Exécuter en tant que **root**

---

## Configuration post-certificat

### Assigner le certificat aux services

1. **Panneau de configuration → Sécurité → Certificat**
2. Cliquer sur **Paramètres**
3. Pour chaque service (DSM, Web Station, VPN Server, etc.), sélectionner le certificat Let's Encrypt dans le menu déroulant
4. Cliquer sur **OK**

### Vérifier le HTTPS

- Accéder au DSM via `https://votre-domaine.com:5001`
- Vérifier que le cadenas apparaît dans le navigateur
- Vérifier la date d'expiration du certificat (clic sur le cadenas → détails)

### Notes sur le renouvellement

| Méthode | Renouvellement | Particularité |
|---------|---------------|---------------|
| DSM intégré | Automatique | Nécessite le port 80 ouvert en permanence |
| acme.sh | Via cron / tâche planifiée | Fonctionne sans port ouvert (DNS-01) |

> Les certificats Let's Encrypt expirent après **90 jours**. Le renouvellement est tenté automatiquement à partir de 30 jours avant l'expiration.

---

## Dépannage

| Problème | Solution |
|----------|----------|
| Échec de validation HTTP-01 | Vérifier que le port 80 est bien redirigé vers le NAS et qu'aucun pare-feu ne bloque |
| Échec de validation DNS-01 | Vérifier les clés API du registrar et que le TXT record se propage (`dig TXT _acme-challenge.votre-domaine.com`) |
| Certificat non renouvelé | Vérifier le cron (`crontab -l`) ou la tâche planifiée DSM |
| Erreur 2FA avec acme.sh | Configurer `SYNO_DEVICE_NAME` et `SYNO_DEVICE_ID` |
