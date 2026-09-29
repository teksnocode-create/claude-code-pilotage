---
name: recap
description: Résume la conversation en cours dans un format prêt à coller dans le /close ("Qu'est-ce que tu as fait aujourd'hui ?"). Se déclenche sur "recap", "/recap" ou "fais un recap".
user-invocable: true
---

# Skill : recap de conversation

## Déclencheur
« recap », « /recap » ou « fais un recap ».

## Objectif
Résumer la conversation en cours dans un format directement injectable dans le `/close` (réponse à « Qu'est-ce que tu as fait aujourd'hui ? »). Utile quand le travail du jour s'est fait dans une autre fenêtre que celle du `/close`.

## Déroulé

### 1. Scanner la conversation en cours
Passer en revue tout ce qui a été échangé dans la session active.

### 2. Produire le bloc de recap

Le bloc complet est enveloppé dans un bloc de code pour être copié-collé tel quel, sans reformatage au collage.

```
Recap : [AAAA-MM-JJ]

Ce qui a été fait :
- [actions concrètes, livrables, décisions prises]

Découvertes / apprentissages :
- [si applicable]

Blocages / points ouverts :
- [si applicable]

Priorité suivante :
- [prochaine action identifiée]
```

### 3. Règles de rédaction
- Factuel, pas de reformulation floue
- Une ligne par point, pas de paragraphes
- Si un projet est clairement identifié, le nommer (par exemple « app de réservation », « SaaS de facturation »)
- Si la conversation est trop courte ou n'a rien de concret : le dire en une phrase

## Ce que ce skill ne fait pas
- Ne crée pas de fichier
- Ne commite pas
- Ne met pas à jour les fichiers de pilotage
- C'est un outil de préparation au `/close`, pas un remplacement
