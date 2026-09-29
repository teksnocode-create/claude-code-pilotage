---
name: relais
description: Passage de témoin vers une nouvelle fenêtre Claude Code, sur n'importe quel projet. Met d'abord le journal du projet à jour (skill log du repo s'il existe), puis produit le prompt de reprise d'une page et le copie dans le presse-papier. Se déclenche sur "relais", "/relais", "fais un relais", "passe le relais" ou "relais vers une nouvelle fenêtre".
user-invocable: true
---

# Skill : relais

## À quoi ça sert

L'utilisateur change de fenêtre Claude Code, en général parce que le contexte est plein. Ce skill
produit **le prompt à coller dans la nouvelle fenêtre** pour qu'elle reprenne le chantier
exactement où il en est, sans repartir de zéro et sans relire toute la session.

C'est un passage de témoin, pas un bilan. `close` s'adresse à l'utilisateur en fin de journée,
`relais` s'adresse à la prochaine fenêtre au milieu du travail.

## Priorité à la version du projet

Si le repo courant a son propre relais (`.claude/skills/relais.md` ou
`.claude/skills/relais/SKILL.md`), le suivre à la place de celui-ci : il connaît les fichiers
propres au projet. Ce skill global sert partout ailleurs.

## Ce qu'il faut faire

### 1. Mettre le journal à jour AVANT d'écrire le prompt

Repérer comment ce projet garde sa mémoire, dans cet ordre :

1. **Un skill `log` dans le repo** (`.claude/skills/log.md` ou `.claude/skills/log/SKILL.md`) :
   le lancer et aller au bout, y compris ses questions à l'utilisateur.
2. **Pas de skill `log`, mais des fichiers de pilotage** (`LOGBOOK.md`, `ROADMAP.md`, un journal
   de session, ou ce que le `CLAUDE.md` désigne comme journal) : y ajouter ce qui a été fait
   dans la session, au format déjà utilisé par le fichier.
3. **Rien de tout ça** : ne rien créer. Le dire en une ligne, et le prompt portera alors
   un peu plus de détail (toujours une page maximum).

C'est l'étape qui compte le plus. Le prompt de relais tient sur une page, la mémoire réelle
du projet vit sur le disque, et c'est ce que la nouvelle fenêtre va lire. Un relais écrit sur
un journal en retard fait perdre la journée.

Si rien de neuf n'est à écrire, continuer sans rien inventer.

### 2. Rassembler l'état réel, pas l'état supposé

- Si c'est un repo git : `git log --oneline -8` (commits du jour, hash court) et
  `git status --short` (ce qui traîne non commité)
- Le `CLAUDE.md` du projet, pour savoir quels fichiers font foi
- Le document de référence en cours (cahier des charges, fiche projet, ROADMAP), s'il y en a un
- Le suivi des tâches propre au projet (ROADMAP, todos, backlog) pour ce qui touche le chantier

Chaque affirmation du prompt doit venir d'un de ces endroits ou de la conversation.
Ne rien déduire.

### 3. Écrire le prompt

En français, avec les accents, dans cet ordre.
Supprimer une section qui n'a rien à dire plutôt que d'y écrire « rien ».

```
On reprend <chantier> (repo ou dossier <nom>), <jour JJ/MM/AAAA>, <moment de la journée>.

## À lire avant de proposer quoi que ce soit
<chemins : CLAUDE.md, document de référence, journal (LOGBOOK, ROADMAP...)>

## Ce qui est déjà fait
<un point par livraison, avec le hash de commit s'il y en a un>
<état des tests ou vérifications, chiffres à l'appui, ou « non vérifié »>

## Ce qui reste
<liste ordonnée, avec la priorité>

## Bloqué, ne pas attendre dessus
<ce qui dépend de quelqu'un d'autre>

## Ce qui attend un arbitrage de l'utilisateur
<les décisions à remonter, jamais à trancher seul>

## Ma méthode, à respecter
<recopier mot pour mot les règles de travail posées par l'utilisateur pendant la session>

Commence par <la prochaine action précise>.
```

### 4. Le mettre dans le presse-papier

Écrire le prompt dans un fichier temporaire, puis le copier :

```bash
pbcopy < <chemin du fichier>        # macOS
xclip -selection clipboard < <chemin du fichier>   # Linux
```

Confirmer en une ligne que c'est copié et prêt à coller.

Puis le recoller aussi en clair dans la réponse, dans un bloc de code : l'utilisateur relit
souvent avant de coller, et une copie silencieuse ne se vérifie pas.

## Règles

- **Le journal d'abord.** On change de fenêtre parce qu'on va perdre le contexte, donc
  le contexte doit être écrit sur le disque avant, pas seulement dans un message.
- **Un fait, une source.** Un commit se cite avec son hash, un chiffre de tests avec le run
  qui l'a produit. Ce qui n'a pas été vérifié se dit non vérifié, en toutes lettres.
- **Recopier la méthode de travail de l'utilisateur telle qu'il l'a énoncée**, pas une
  reformulation. C'est la partie que la nouvelle fenêtre ne peut deviner d'aucun fichier.
- **Une page maximum.** Au-delà, la nouvelle fenêtre lit un pavé au lieu de lire le repo.
  Le détail vit dans le journal, le prompt dit seulement où regarder.
- **Finir par une action précise**, jamais par « continue le travail ».
- Ne rien pousser, ne rien commiter au titre du relais. Seule l'étape 1 écrit, et uniquement
  dans les fichiers de pilotage du projet.
