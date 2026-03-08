# Task List — Infrastructure Maison

## En cours

- [ ] **Automatiser le déploiement du certificat sur NAS01** — Configurer le deploy hook acme.sh avec le compte `certadmin` (sans 2FA)

## À faire

- [ ] **Configurer la gestion des mots de passe** — Trouver une solution pour stocker les secrets de façon sécurisée
- [ ] **Activer la redirection HTTPS sur NAS01** — DSM ne redirige pas HTTP→HTTPS actuellement
- [ ] **Activer HSTS sur NAS01** — Renforcer la sécurité TLS
- [ ] **Passer SMB min protocol à SMB2** — NT1 (SMBv1) est encore autorisé, risque de sécurité
- [ ] **Renforcer la politique de mots de passe NAS01** — Ajouter complexité (majuscules, chiffres, spéciaux)
- [ ] **Créer le record DNS hs.fstgermain.com** — Présent dans la config DDNS mais pas encore créé
- [ ] **Documenter le réseau** — Routeur, switch, Wi-Fi, plan d'adressage IP
- [ ] **Documenter la domotique** — Home Assistant, objets connectés
- [ ] **Documenter l'électricité / plomberie** — Plans, notes techniques
- [ ] **Configurer le deploy hook acme.sh pour NAS01** — Automatiser le renouvellement du cert sur le NAS (nécessite 2FA device ID)

## Complété

- [x] **Créer le dépôt home sur GitHub** — 2026-03-08
- [x] **Documenter la config NAS01** — Export DSM analysé, 7 fichiers de doc créés — 2026-03-08
- [x] **Générer le certificat wildcard *.fstgermain.com** — acme.sh + Cloudflare DNS-01 — 2026-03-08
- [x] **Installer acme.sh sur Windows** — Avec plugins dnsapi et tâche planifiée — 2026-03-08
- [x] **Déployer le certificat wildcard sur NAS01** — Import manuel via DSM, défini comme certificat par défaut — 2026-03-08
- [x] **Créer le compte certadmin sur NAS01** — Compte admin sans 2FA pour le deploy hook futur — 2026-03-08
