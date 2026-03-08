# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Documentation centralisée pour l'infrastructure maison de Denis St-Germain : réseau, NAS Synology, domotique, certificats, DNS, etc.

## Workflow obligatoire

À chaque intervention sur l'infrastructure :

1. **Exécuter** la tâche technique demandée
2. **Documenter** dans le dossier approprié (créer si nécessaire)
3. **Mettre à jour** `TODO.md` (tâches complétées, nouvelles tâches)
4. **Mettre à jour** la mémoire persistante (`memory/`) avec les nouvelles connaissances
5. **Committer et pousser** sur GitHub

## Structure

- `certificats/` — Certificats SSL/TLS (wildcard *.fstgermain.com)
- `nas/nas01/` — Configuration du NAS Synology DS918+
- `reseau/` — Configuration réseau (à venir)
- `domotique/` — Home Assistant et objets connectés (à venir)
- `TODO.md` — Task list de l'infrastructure
- `newcontent/` — Fichiers source bruts (gitignored)

## Conventions

- Langue : **français**
- Format : Markdown (`.md`)
- Chaque appareil/sujet a son propre dossier avec un `README.md`
- Ne jamais committer : mots de passe, hash, tokens API, clés privées
- Projets connexes : `D:\GithubRepo\cloudflare\` (DDNS Cloudflare)

## Infrastructure connue

- **Domaine** : fstgermain.com (DNS Cloudflare)
- **NAS01** : Synology DS918+, DSM 7.2, IP 10.0.0.105
- **Certificat** : Wildcard *.fstgermain.com (acme.sh, Let's Encrypt)
- **DDNS** : Service custom Node.js pour Cloudflare
