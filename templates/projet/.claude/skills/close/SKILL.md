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
