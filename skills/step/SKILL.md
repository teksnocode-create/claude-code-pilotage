---
name: step
description: Traite une tâche complexe en mode pas à pas. Découpe en étapes atomiques, langage simple sans jargon, une seule étape à la fois avec validation explicite avant de passer à la suivante. S'applique à tout type de tâche (code, config, admin, démarche). Se déclenche sur "step", "/step", "vas-y étape par étape" ou "explique-moi pas à pas".
user-invocable: true
---

# Skill : step, explication pas à pas

Pour une tâche que l'utilisateur ne maîtrise pas et qu'il ne veut pas subir d'un bloc. L'objectif n'est pas d'aller vite, c'est qu'il comprenne et valide chaque étape avant la suivante.

## Déclencheur
- **Explicite uniquement** : « step », « /step », « vas-y étape par étape », « explique-moi pas à pas », ou équivalent.
- Pas de déclenchement automatique sur une tâche jugée « complexe » par Claude : c'est l'utilisateur qui décide quand il veut ce mode, pas une supposition sur son niveau.
- Reste actif pour toute la tâche en cours, jusqu'à ce qu'elle soit terminée ou que l'utilisateur dise d'arrêter (« fini le pas à pas », « vas-y normalement »).

## Objectif
Faire avancer une tâche complexe (technique ou non) par étapes atomiques, validées une par une, sans jargon non expliqué.

## Déroulé

### 1. Découper la tâche avant de commencer
Identifier la suite d'étapes nécessaires. Une étape = une seule action ou une seule notion. Si une étape contient un « et » (faire X et Y), c'est deux étapes.

Annoncer en une phrase le nombre approximatif d'étapes avant de commencer, sans détailler tout le plan à l'avance (ça redevient un pavé).

### 2. Traiter une étape à la fois
Pour chaque étape :
- Expliquer ce qu'on fait et pourquoi, en langage simple (pas de jargon technique sans le traduire immédiatement dans une logique que l'utilisateur connaît déjà).
- Exécuter uniquement cette étape, jamais la suivante, même si la suite est évidente.
- Terminer par un résumé d'une phrase de ce qui vient d'être fait.
- Poser une question fermée : « OK, on passe à l'étape suivante ? »

### 3. Attendre la validation
Ne jamais enchaîner sans confirmation explicite. Un silence ou une réponse ambiguë n'est pas une validation : redemander.

Si l'utilisateur signale un problème ou une incompréhension sur l'étape en cours : rester dessus, reformuler autrement (nouvelle analogie, découpage plus fin), ne pas avancer tant que ce n'est pas clair.

### 4. Clôturer
À la dernière étape, le dire explicitement (« dernière étape ») et faire un récap final très court de ce qui a été fait au total.

## Ce que ce skill ne fait pas
- Ne devine jamais que l'utilisateur a compris : la validation est toujours explicite, jamais supposée.
- Ne groupe jamais plusieurs étapes pour « gagner du temps ». Si l'utilisateur veut aller plus vite, il le dit et on quitte le mode pas à pas.
- Ne fixe pas de nombre d'étapes à l'avance : la granularité s'ajuste à la tâche, pas à un format standard.
