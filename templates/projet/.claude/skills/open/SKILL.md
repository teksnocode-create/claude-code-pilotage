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
