---
name: new-project
description: Initialise la structure complète d'un nouveau repo de projet (CLAUDE.md, ROADMAP.md, LOGBOOK.md, .gitignore adapté à la stack, skills projet open/log/close, checklist OWASP), puis mène l'interview section par section pour les remplir. Déclencher sur "/new-project", "init projet", "nouveau projet", "initialise ce projet", "setup projet", ou à l'ouverture d'un repo vide pour démarrer un chantier.
---

# Skill : /new-project, initialisation d'un nouveau projet

## Déclencheur
`/new-project`, "init projet", "nouveau projet", "initialise ce projet", "setup projet".

## Objectif
En 3 phases, créer la structure complète d'un nouveau projet :
- `CLAUDE.md` : contexte projet pour Claude Code
- `ROADMAP.md` : phases et périmètre MVP
- `LOGBOOK.md` : journal de sessions
- `.claude/skills/` : `open`, `log`, `close`, propres à ce repo
- `.claude/rules/owasp-checklist.md` : toujours présente
- `.gitignore` : adapté à la stack détectée

---

## Phase 1 : créer le squelette

Avant toute question, créer immédiatement la structure suivante (fichiers vides ou avec placeholder) :

```
CLAUDE.md               # rempli en Phase 3
ROADMAP.md              # rempli en Phase 3
LOGBOOK.md              # rempli en Phase 3
.gitignore              # rempli selon la stack détectée
.claude/
  rules/
    .gitkeep
  skills/
    .gitkeep
docs/
  .gitkeep
```

Confirmer : « Structure créée. Je commence l'interview, une section à la fois. »

---

## Phase 2 : interview, une section à la fois

Poser chaque section séparément. Attendre la réponse avant de passer à la suivante.
Si l'utilisateur dit « passe » ou « plus tard » : noter un placeholder dans le fichier concerné et avancer.

### Section 1 : le projet
- Nom du projet ?
- Type : SaaS / app mobile / automatisation / site vitrine / CRM / outil interne / autre ?
- En une phrase : quel problème ça résout, pour qui ?
- Projet client ou projet perso ?
- Repo GitHub déjà créé ? URL si oui ?
- Tu es seul sur ce repo, ou plusieurs personnes y travaillent ? (détermine la variante du `/close` généré)

### Section 2 : stack technique
- Front ? (Next.js, React, Vue, Lovable, FlutterFlow, aucun, autre)
- Back / BDD ? (Supabase, Airtable, Firebase, aucun, autre)
- Auth ? (Supabase Auth, Clerk, NextAuth, aucune, autre)
- Déploiement ? (Vercel, Netlify, VPS, App Store, Play Store, autre)
- Automatisation ? (n8n, Make, aucune, autre)
- Autres services ou APIs à intégrer ? (Stripe, OpenAI, Brevo, etc.)

### Section 3 : MVP, périmètre
- Les 3 à 5 features du MVP (ce qui est IN) ?
- Ce qui est explicitement hors scope (pour ne pas dériver) ?
- Une deadline ou date cible ?

### Section 4 : données et sécurité
- Tables principales et leur rôle, une ligne chacune ?
- Données sensibles à ne jamais exposer côté client ? (clés API, tokens, secrets de webhook)
- Accès : public / avec login utilisateur / admin uniquement ?
- Supabase avec de l'auth ou des données utilisateurs sensibles ? (oui / non) Si oui, les règles de sécurité avancées sont activées en Phase 3.

### Section 5 : déploiement et conventions
- Déploiement automatique (push vers Vercel) ou manuel (CLI) ?
- Conventions de code : TypeScript strict ? ESLint ? Nommage particulier ?
- Langue du code et des commentaires : FR ou EN ?

---

## Phase 3 : générer les fichiers

À partir des réponses, remplir les gabarits ci-dessous dans cet ordre. Remplacer chaque `[...]` par la réponse correspondante, et `[NOM]` par le nom du projet.

**Déclenchement sécurité :** si la section 4 indique Supabase + auth OU données sensibles, générer aussi `.claude/rules/security-supabase.md` et le référencer dans CLAUDE.md. Sinon, retirer la ligne correspondante de CLAUDE.md.

### CLAUDE.md
~~~markdown
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
~~~

### ROADMAP.md
~~~markdown
# ROADMAP : [Nom du projet]

_Dernière mise à jour : [AAAA-MM-JJ]_

## Phase 0 : Setup (fait)
- [x] Init projet : CLAUDE.md, ROADMAP.md, LOGBOOK.md, skills open/log/close

## Phase 1 : MVP
- [ ] [feature 1]
- [ ] [feature 2]
- [ ] [feature 3]

**Deadline MVP** : [date ou "non définie"]

## Phase 2 : Post-MVP
_(à définir après livraison du MVP)_

## Hors scope : ne pas dériver
- [ce qui est explicitement exclu, avec la raison]
~~~

### LOGBOOK.md
~~~markdown
# LOGBOOK : [Nom du projet]

Journal chronologique des sessions. Une entrée par session, append-only : on ajoute à la suite, on ne réécrit jamais une entrée passée.

---

## [AAAA-MM-JJ] : Session 0, init projet

**Fait**
- Structure projet initialisée (CLAUDE.md, ROADMAP.md, LOGBOOK.md)
- Stack définie : [résumé]
- MVP cadré : [nb] features, deadline [date ou "non définie"]

**Décisions**
- [toute décision structurante prise pendant le cadrage]

**Prochaine étape**
- [première feature du MVP ou première tâche concrète]
~~~

### .claude/skills/ : open, log, close (systématique)

Générer les 3 dans **tous** les projets. Ils appartiennent à ce repo : les modifier ici ne touche aucun autre projet, et sur un repo partagé ils portent le process de l'équipe.
Le `/close` a deux variantes selon la réponse « seul ou à plusieurs » de la section 1 : en solo, supprimer la ligne `[VARIANTE MULTI-PERSONNES ...]` ; à plusieurs, la garder sans les crochets.

#### `.claude/skills/open/SKILL.md`
~~~markdown
---
name: open
description: Reprise de session sur [NOM]. Affiche où en est le projet, ce qui est en cours et ce qui traîne non commité. Déclencher sur "/open", "on reprend", "où on en est".
---

# /open : [NOM]

## Déroulé

### 0. Vérifier GitHub avant tout
Du travail a pu être poussé depuis une autre machine ou depuis Claude Code sur mobile ou web. Sans cette étape, l'open se construit sur une copie périmée.
1. `git fetch --all --prune`
2. `git log --oneline main..origin/main` : commits présents sur GitHub mais pas ici
3. `git branch -r --no-merged main | grep origin/claude/` : branches ouvertes par Claude Code distant, jamais fusionnées

S'il y a quelque chose : l'afficher **en tête de la sortie** (branche, nombre de commits, date et message du dernier) et proposer de rapatrier (`git pull --ff-only` pour main, merge branche par branche pour `claude/*`). **Ne rien fusionner sans le oui de l'utilisateur.**
Si rien : une ligne « GitHub : à jour ». Si le fetch échoue (pas de réseau) : le dire en une ligne et continuer.

### 1. Lire les fichiers de pilotage, en direct
1. `ROADMAP.md` : phase en cours, features cochées, features restantes
2. Les 3 dernières entrées de `LOGBOOK.md` : ce qui a été fait, la prochaine étape notée la dernière fois
3. `git status` et `git log --oneline -5` : travail non commité, derniers commits, branche courante

## Sortie
```
OPEN : [NOM] : [date, jour de la semaine]
Où on en est : phase [X], [N] features sur [M]
Dernière session : [date], [résumé en une ligne]
Prochaine étape notée : [reprise du LOGBOOK]
Non commité : [fichiers, ou "rien"]
```

## Règles
- Lire les fichiers en direct, ne jamais se fier à la mémoire de la conversation
- Si `LOGBOOK.md` est vide, le dire au lieu d'inventer
- Ne rien modifier : `/open` est en lecture seule
~~~

#### `.claude/skills/log/SKILL.md`
~~~markdown
---
name: log
description: Snapshot de la conversation en cours dans le LOGBOOK de [NOM], pour fermer une fenêtre sans perdre le fil. Déclencher sur "/log", "note ce qu'on a fait", "archive ça".
---

# /log : [NOM]

## Déroulé
1. Extraire de la conversation : ce qui a été produit, les décisions structurantes, la prochaine étape concrète
2. Ajouter à la suite de `LOGBOOK.md` :

```
### [HH:MM] : [sujet en 3 à 5 mots]

**Fait**
- [5 puces maximum, synthétisées]

**Décisions**
- [uniquement ce qui engage la suite, sinon "aucune"]

**Prochaine étape**
- [une seule, la plus immédiate]
```

3. Si une feature de `ROADMAP.md` est réellement livrée, la cocher

## Règles
- 5 puces maximum dans « Fait » : synthétiser, pas tout lister
- Rien ne se coche « livré » sans preuve : un commit, un test passé, une vérification faite dans la session. Sinon, écrire « non vérifié »
- Ne pas commiter, ne pas pousser : `/log` écrit un fichier, c'est tout
- Si la session a déjà une entrée du jour, compléter sous le même titre de date
~~~

#### `.claude/skills/close/SKILL.md`
~~~markdown
---
name: close
description: Clôture de session sur [NOM] : bilan, LOGBOOK, ROADMAP, contrôle de ce qui part sur GitHub, commit et push. Déclencher sur "/close", "on ferme", "fin de session".
---

# /close : [NOM]

## Étape 0 : le cadre
Date du jour et jour de la semaine.
[VARIANTE MULTI-PERSONNES : demander le prénom de la personne au clavier, il apparaît dans l'entrée du LOGBOOK et dans le message de commit.]

## Étape 1 : le bilan, avant toute question
Produire le bilan à partir de la conversation et du `git diff`, puis le soumettre pour correction. Ne pas demander « qu'est-ce que tu as fait ? » à quelqu'un qui vient de le faire.

Trois blocs : **fait aujourd'hui**, **en cours / points ouverts**, **bloqué, en attente de quelqu'un**.

## Étape 2 : écrire dans `LOGBOOK.md`
Une entrée par session, append-only, jamais de réécriture d'une entrée passée.

## Étape 3 : mettre à jour `ROADMAP.md`
Cocher ce qui est livré. Ajouter ce qui est apparu en cours de route. Si une feature sort du périmètre, la déplacer en « Hors scope » avec la raison, ne pas la supprimer.

## Étape 4 : contrôle de ce qui part sur GitHub
Avant tout commit, vérifier ligne par ligne dans le diff :
- Aucun secret, clé d'API, token ni clé de service
- `.env` bien ignoré, aucun fichier d'identifiants indexé
- Aucune donnée client réelle, aucun identifiant, aucune adresse
- Aucun export ni dump de base

Un doute sur un fichier se traite avant le commit, pas après le push.

## Étape 5 : la sécurité, si quelque chose part en production
Si la session met quelque chose en ligne ou touche à l'authentification, aux permissions ou aux données utilisateurs, repasser `.claude/rules/owasp-checklist.md` et reporter les points non traités avec leur raison.

## Étape 6 : commit et push
`git add` ciblé (jamais `git add .` à l'aveugle), commit, `git pull --rebase`, `git push`. En cas de conflit, le résoudre fichier par fichier et le signaler, ne jamais forcer.

## Étape 7 : la sortie
Une ligne : ce qui est poussé, et la prochaine étape.

## Règles
- Le bilan se propose, il ne se demande pas
- `LOGBOOK.md` est append-only
- Rien ne part sur GitHub sans l'étape 4
~~~

### .claude/rules/owasp-checklist.md (systématique)

Générer sur **tous** les projets, sans condition, même sans Supabase et sans auth. Dix questions coûtent 10 minutes, une fuite de données entre clients coûte le client.

~~~markdown
# Checklist OWASP Top 10:2025

Source : https://top10.owasp.org/2025/

## Quand la repasser
- Avant chaque mise en production
- Dès qu'on touche à l'authentification, aux permissions ou aux données utilisateurs
- Dès qu'on ajoute une dépendance ou un service externe

Une ligne qui n'est pas cochée n'est pas un détail à traiter plus tard : c'est une décision à prendre et à écrire.

## Les 10 points

- [ ] **A01 Broken Access Control** : un compte connecté peut-il lire ou modifier les données d'un autre compte ? Tester en conditions réelles avec deux comptes, pas en lisant le code. *Cas typique : une table sans règle d'écriture qui reste ouverte des jours sans que personne ne le voie.*
- [ ] **A02 Security Misconfiguration** : `.env` bien ignoré par git, aucune clé de service côté client, pas de compte ni de mot de passe par défaut laissé actif.
- [ ] **A03 Software Supply Chain Failures** : d'où viennent les dépendances et les templates utilisés, et qui peut pousser du code qui part en production ?
- [ ] **A04 Cryptographic Failures** : quelles données sensibles sont stockées, et sous quelle forme ? Aucun secret, aucun code d'accès en clair dans le dépôt ni dans un document qui circule (captures d'écran et documentation comprises).
- [ ] **A05 Injection** : toute entrée utilisateur est validée côté serveur, jamais concaténée dans une requête. Vaut aussi pour les entrées passées à un modèle IA.
- [ ] **A06 Insecure Design** : le scénario d'abus a-t-il été posé avant de coder ? Qui a intérêt à tricher ici, et qu'est-ce qui l'en empêche ?
- [ ] **A07 Authentication Failures** : comment on se connecte, comment on se déconnecte partout, et que vaut réellement le facteur utilisé (un code à 4 chiffres n'est pas une authentification).
- [ ] **A08 Software or Data Integrity Failures** : que se passe-t-il si une automatisation écrase une donnée saisie à la main ? Qui gagne en cas de conflit, et c'est écrit où ?
- [ ] **A09 Security Logging and Alerting Failures** : si ça tombe en panne cette nuit, qui l'apprend et au bout de combien de temps ? Une alerte que personne n'ouvre ne compte pas comme une alerte. *Cas typique : des relances automatiques en panne une semaine sans aucun signal.*
- [ ] **A10 Mishandling of Exceptional Conditions** : que fait le système quand l'API externe ne répond pas, renvoie une erreur ou des données vides ? Un échec silencieux est pire qu'un plantage.

## Règle
Les points non traités restent listés ici avec la raison et la date, jamais effacés.
~~~

### .claude/rules/security-supabase.md (conditionnel)

Uniquement si Supabase + auth OU données sensibles confirmés en section 4.

~~~markdown
# Règles de sécurité : Supabase + Auth

<!-- Gabarit conditionnel : à garder seulement si le projet utilise Supabase avec de l'auth ou des données sensibles. -->

## Patterns API : obligatoires sur chaque endpoint

- **IDOR** : vérification atomique sur toute opération sensible, `WHERE id=$1 AND user_id=$2`
- **Race conditions** : `SELECT ... FOR UPDATE` sur les ressources partagées
- **Rate limiting** : fail-closed en prod sur login, exports, endpoints IA
- **Tokens** : comparaison avec `crypto.timingSafeEqual()`, jamais `===`
- **Inputs** : validation Zod avec `.strict()` obligatoire, whitelist explicite, pas de passthrough
- **Pagination** : limite dure côté serveur sur toutes les listes, jamais illimitée
- **Secrets** : jamais en dur, `import.meta.env` (front) et `process.env` (back) uniquement

## Authentification & sessions

- Tokens stockés exclusivement en cookies `HttpOnly, Secure, SameSite=Strict`
- `localStorage` et `sessionStorage` interdits pour tout token ou donnée de session
- Champ `sessionVersion` dans le profil pour permettre la déconnexion globale
- Vérification en base des tokens révoqués

## Supabase & base de données

- **RLS obligatoire** sur toutes les tables : pas de `FOR ALL`, pas de table sans politique
- Optimiser les politiques avec `(select auth.uid())` pour éviter les appels répétés
- Rôle `anon` : politiques restrictives par défaut, refuser si pas de règle explicite
- Fonctions PL/pgSQL avec `SET search_path = ''` pour éviter le détournement de schéma
- Extensions installées dans un schéma `extensions` dédié (jamais dans `public`)
- Triggers en écriture sur les colonnes sensibles : `updated_at`, `role`, `sessionVersion`
- Table `audit_logs` pour tracer les actions critiques : acteur, table, diff JSON, horodatage

## IA & agents LLM (si applicable)

- Encadrer les entrées utilisateurs avec des balises explicites : `<user_input>...</user_input>`
- Valider et assainir (XSS) les sorties des LLM avant affichage ou stockage
- Les actions IA opèrent avec le token de l'utilisateur (limité par son RLS)
- Jamais de clé de service pour une action déclenchée par un agent IA
~~~

### .gitignore

Générer selon la stack détectée en section 2. Base systématique :

```
.env
.env.local
.env*.local
CLAUDE.local.md
.claude/settings.local.json
node_modules/
.DS_Store
```

Ajouter selon la stack :
- Next.js : `.next/`, `out/`
- Vercel : `.vercel/`
- Supabase : `.supabase/`
- Python : `__pycache__/`, `*.pyc`, `.venv/`

---

## Étape finale

Une fois les fichiers générés :

1. Afficher l'arborescence complète des fichiers créés
2. Résumé en une ligne par fichier (préciser si `security-supabase.md` a été activé ; `owasp-checklist.md` et les 3 skills `open` / `log` / `close` sont toujours présents)
3. Créer le premier commit git : `feat: init projet [nom], structure et fichiers de pilotage`
4. Demander : « Tu veux qu'on attaque quelle feature en premier ? »

---

## Règles pour Claude

- Créer le squelette de la Phase 1 AVANT de poser la moindre question
- Poser les sections UNE PAR UNE, jamais toutes les questions d'un coup
- Si « passe » ou « plus tard » : placeholder dans le fichier, on avance
- CLAUDE.md sous 120 lignes : si ça déborde, c'est qu'on y met trop de choses
- Pas de contenu dupliqué entre CLAUDE.md et ROADMAP.md : chaque info a une seule maison
- Les seuls skills générés au setup sont `open`, `log` et `close`, propres à ce repo. Ne pas en créer d'autres tant qu'un workflow récurrent n'a pas émergé
- Ne jamais transformer ces 3 skills en skills globaux : sur un repo partagé, ils portent le process de l'équipe et une version globale l'écraserait pour tout le monde
- Si le repo GitHub n'existe pas encore : ne pas bloquer, noter « non créé » dans CLAUDE.md et avancer
