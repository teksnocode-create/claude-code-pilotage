---
name: lis
description: Force la lecture intégrale d'un document long avant toute action, puis bloque sur un résumé en langage clair validé par l'utilisateur avant d'écrire du code. Déclencher UNIQUEMENT sur "/lis" ou "lis tout" explicite, jamais automatiquement sur simple ajout d'un fichier volumineux.
---

# Skill : lis

Skill à déclenchement explicite. Objectif : éliminer le risque de lecture partielle ou de résumé de surface sur un document long (cahier des charges, brief client, spec technique, contrat) avant de s'engager sur du code ou une architecture.

Ne s'active QUE si l'utilisateur tape `/lis` ou `lis tout`. Sur simple ajout de fichier sans ce mot-clé, comportement normal.

## Pourquoi ce skill existe

Les outils de lecture tronquent souvent les gros fichiers : ils gardent le début et la fin, et coupent le milieu. Sur un document de 30 à 50 pages, une section entière du milieu peut être invisible sans que ça se voie. Ce skill impose une lecture séquentielle complète, bloc par bloc, pour éliminer ce trou.

## Protocole

### 1. Identifier le document et sa taille

- Localiser le fichier au chemin fourni
- Si docx ou pdf : en extraire d'abord le texte brut (skill `docx` / `pdf`, ou outil équivalent)
- Mesurer la taille (caractères ou pages) avec `wc` ou équivalent

### 2. Lecture séquentielle par blocs

- Découper en blocs d'environ 8 à 10k caractères (lecture par plages de lignes, ou par tranches en bash)
- Lire CHAQUE bloc dans l'ordre, sans sauter
- Après chaque bloc, noter en interne (pas besoin de l'afficher) : faits, contraintes, chiffres, deadlines, exigences techniques rencontrés
- Ne jamais s'arrêter avant d'avoir couvert 100 % du fichier

### 3. Restitution obligatoire : deux blocs, langage business

Une fois la lecture complète terminée, produire dans le chat, sans jargon technique :

**Ce que j'ai compris du document**
- Reformulation factuelle : qui, quoi, contraintes, chiffres, deadlines
- Pas une paraphrase du plan du document, une synthèse dans mes mots

**Ce que je propose de faire**
- Plan d'action concret en réponse au document, en langage simple
- Si le document contient des zones ambiguës ou contradictoires, les signaler ici plutôt que de trancher seul

### 4. Stop total

Après la restitution, fin du tour. Ne pas écrire une ligne de code, ne pas créer de fichier, ne pas toucher à une architecture tant que l'utilisateur n'a pas donné un go explicite. Pas de « je commence en attendant ta validation » : arrêt complet.

Si l'utilisateur répond avec des corrections plutôt qu'un go, les intégrer et redemander validation avant de coder.
