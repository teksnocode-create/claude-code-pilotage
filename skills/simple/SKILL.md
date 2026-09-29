---
name: simple
description: Refait la dernière réponse courte ET sans jargon. Coupe les pavés trop longs et retraduit le vocabulaire technique au niveau réel de l'utilisateur (profil no-code / IA, logique n8n, Make, Airtable, Supabase, pas de vocabulaire dev formel). Se déclenche sur "simple", ou se propose spontanément après une réponse trop longue ou chargée en jargon non expliqué.
user-invocable: true
---

# Skill : simple, court et sans jargon

Deux choses font décrocher : les termes techniques non expliqués, et les pavés. Ce skill traite les deux d'un coup, sur un seul mot.

## Déclencheur
- **Explicite** : l'utilisateur dit « simple » (ou « /simple ») après une réponse.
- **Spontané** : juste après une réponse trop dense, proposer en une ligne, à la fin : « Je peux te la refaire courte et sans jargon, tape "simple". » Pas à chaque réponse technique : seulement quand c'est réel, plusieurs termes non expliqués dans le même message ou une réponse qui dépasse un écran.

## Objectif
Renvoyer la même information, mais lisible d'un coup d'œil : dans le langage de l'utilisateur (il pense en logique n8n / Make / Airtable / Supabase / API, pas en vocabulaire dev formel) et dans un format qu'il lit en entier.

## Déroulé

### 1. Identifier ce qu'il faut refaire
Reprendre la dernière réponse substantielle de la conversation, sauf si l'utilisateur désigne un autre passage.

### 2. Couper le pavé
- **5 lignes maximum**, sauf si le fond est réellement irréductible.
- **Commencer par la conclusion** : ce qu'il faut retenir ou faire, en première phrase. Le raisonnement vient après, ou pas du tout.
- **Une seule idée par paragraphe.** Si la réponse d'origine empilait plusieurs sujets, n'en garder qu'un et lister les autres en une ligne : « Il y avait aussi X et Y, dis-moi si tu veux que je les reprenne. »
- **3 puces maximum.** Au-delà, c'est que le contenu doit être découpé, pas listé.
- Supprimer : les rappels de contexte déjà connus, les précautions, les alternatives non retenues, les répétitions.

### 3. Enlever le jargon
Pour chaque terme technique non expliqué :
- Vérifier d'abord s'il est dans `glossaire.md` (même dossier) : si oui, il est acquis, ne pas le re-simplifier, l'utiliser tel quel.
- S'il existe un équivalent naturel dans la stack de l'utilisateur (n8n, Make, Airtable, Supabase, API / webhook, prompt / agent IA) : traduire par analogie avec ça, pas par une définition abstraite.
- Sinon : une ligne de définition simple, intégrée naturellement dans la phrase, pas un glossaire à part dans la réponse.
- Ton direct, professionnel, jamais condescendant, pas de posture « expliqué comme à un enfant ».

### 4. Tenir le glossaire
Après toute retraduction, mettre à jour `glossaire.md` :
- Ajouter les nouveaux termes traités, format `- **terme** : explication courte utilisée`.
- Ce fichier sert de mémoire du niveau réel de l'utilisateur : plus il grandit, moins il faut simplifier, et plus ces termes peuvent être utilisés directement dans les réponses normales.

## Ce que ce skill ne fait pas
- **Ne coupe jamais dans le fond** : les chiffres, les verdicts, les risques, les décisions et les échéances restent tous. On coupe le remplissage et le vocabulaire, jamais l'information qui change une décision. Si raccourcir obligeait à supprimer un fait qui compte, garder le fait et couper ailleurs.
- Ne remplace pas l'explication technique initiale (utile pour en reparler avec un profil dev).

## Note
Le vrai correctif est en amont : une règle anti-pavé permanente dans le `CLAUDE.md` global (`~/.claude/CLAUDE.md`, section « Format de réponse ») s'applique à toutes les réponses sans rien taper. Ce skill est le rattrapage quand la règle n'a pas suffi.
