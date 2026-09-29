# CLAUDE.md : [Nom du projet]

> [Le problème résolu, en une phrase]

<!-- Gabarit. Rester sous 120 lignes : au-delà, c'est qu'on y met trop de choses. -->

## Stack technique
- **Front** : [ex. Next.js, Lovable, aucun]
- **Back / BDD** : [ex. Supabase, Airtable]
- **Auth** : [ex. Supabase Auth, aucune]
- **Déploiement** : [ex. Vercel, App Store]
- **Automatisation** : [ex. n8n, Make, aucune]
- **Repo** : [URL ou "non créé"], branche principale : `main`

## Déploiement
**État actuel** : [auto / manuel / non configuré]

## Sécurité : règles absolues
- Ne jamais exposer [données sensibles] côté client ni dans le repo
- [autres règles propres au projet]
- Checklist OWASP Top 10 à repasser avant toute mise en production : voir `.claude/rules/owasp-checklist.md`
- [Si Supabase + auth ou données sensibles] Règles détaillées : voir `.claude/rules/security-supabase.md`

## Modèle de données
| Table | Rôle |
|---|---|
| [table] | [rôle en une ligne] |

## Intégrations externes
- [service] : [rôle], appelé côté [serveur / client]

## Skills Claude : quand les proposer
- **/qa** : quand une feature est déclarée terminée, avant déploiement
- **/investigate** : dès qu'une erreur ou un comportement inattendu est mentionné
- **/review** : avant tout commit sur `main` touchant l'auth, les règles d'accès ou les actions serveur
- **/security-review** : dès qu'une modif touche l'auth, les permissions ou des données sensibles

## Pilotage
- **ROADMAP.md** : état d'avancement par phases, source de vérité
- **LOGBOOK.md** : journal chronologique des sessions
- `/open` en début de session, `/log` en cours de route, `/close` en fin de session

## Conventions
- Langue du code et des commentaires : [FR / EN]
- [TypeScript strict / ESLint / nommage]

## Mots-clés projet
<!-- `/open`, `/log` et `/close` appartiennent à ce repo : les modifier ici ne touche aucun autre projet -->
<!-- Format : `mot-clé` : ce que ça fait -->
