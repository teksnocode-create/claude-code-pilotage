# Système de pilotage Claude Code

Des skills et des gabarits pour que Claude Code garde le fil d'un projet d'une session à l'autre.

## Le problème

Claude Code ne se souvient de rien entre deux sessions. Chaque nouvelle fenêtre repart de zéro : il faut réexpliquer où on en est, ce qui a été décidé, ce qui reste à faire. Et quand une session devient trop longue, le contexte sature et on perd le fil au milieu du travail.

Résultat : du temps perdu à chaque reprise, des décisions oubliées, des tâches refaites deux fois.

## La réponse

La mémoire du projet ne vit pas dans la conversation, elle vit **sur le disque**, dans trois fichiers que Claude lit et met à jour lui-même :

| Fichier | Rôle |
|---|---|
| `CLAUDE.md` | La fiche d'identité du projet : stack, règles, conventions. Lue automatiquement à chaque session. |
| `ROADMAP.md` | Où en est le projet : phases, features faites et à faire, ce qui est hors scope. |
| `LOGBOOK.md` | Le journal de bord : une entrée par session, ce qui a été fait, décidé, et la prochaine étape. |

Autour de ces fichiers, un cycle de quatre commandes :

```
   /open  ──────►  travail  ──────►  /close
     ▲               │   ▲              │
     │           /log│   │              │
     │               ▼   │              │
     │           LOGBOOK / ROADMAP      │
     │               │                  │
     │           /relais                │
     │   (fenêtre pleine : nouvelle     │
     │    fenêtre, même chantier)       │
     │                                  │
     └──────── session suivante ◄───────┘
```

- **/open** lit ROADMAP, LOGBOOK et l'état git, et dit en cinq lignes où on en est.
- **/log** note ce qui vient d'être fait dans le LOGBOOK, sans commiter.
- **/relais** met le journal à jour puis écrit le prompt d'une page à coller dans une nouvelle fenêtre.
- **/close** fait le bilan, met à jour LOGBOOK et ROADMAP, vérifie qu'aucun secret ne part, puis commit et push.

À cela s'ajoutent des skills de communication, pour que les réponses restent lisibles et que rien ne se fasse à l'aveugle.

## Les skills

**Pilotage**
- `new-project` : initialise un nouveau repo (CLAUDE.md, ROADMAP, LOGBOOK, skills open / log / close, checklist sécurité OWASP) en menant une courte interview.
- `relais` : passage de témoin vers une nouvelle fenêtre, journal d'abord, puis prompt de reprise copié dans le presse-papier.
- `recap` : résume la conversation en cours dans un bloc prêt à coller dans le `/close`.

**Communication**
- `simple` : refait la dernière réponse en 5 lignes, sans jargon, avec des analogies n8n / Make / Airtable / Supabase, et tient un glossaire des termes déjà acquis.
- `step` : mode pas à pas, une étape à la fois, validée avant de passer à la suivante.
- `lis` : oblige Claude à lire un long document en entier, puis à résumer et attendre un go avant d'écrire du code.

**Gabarits de projet** (`templates/projet/`)

Les fichiers que `new-project` génère, lisibles et copiables à la main : `CLAUDE.md`, `ROADMAP.md`, `LOGBOOK.md`, les skills `open`, `log` et `close`, la checklist OWASP Top 10 et les règles de sécurité Supabase. Les skills `open`, `log` et `close` vivent **dans chaque repo**, pas en global : chaque projet peut adapter les siens.

## Installer

Les skills globaux se copient dans `~/.claude/skills/` :

```bash
git clone <url-de-ce-repo> claude-code-pilotage
cp -R claude-code-pilotage/skills/* ~/.claude/skills/
```

Ensuite, dans un repo vide, lance Claude Code et tape `/new-project`. Pour un projet existant, copie le contenu de `templates/projet/` à la racine du repo et remplis les `[...]`.

Les skills sont en français et se déclenchent sur des mots simples (« on reprend », « relais », « simple », « step »). Adapte les descriptions à ta façon de parler.

---

Utilisé au quotidien sur 13 projets (SaaS, apps, missions clients). Portfolio : https://lab.sorek-inc.fr
