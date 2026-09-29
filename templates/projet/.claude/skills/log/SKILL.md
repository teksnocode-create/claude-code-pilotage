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
