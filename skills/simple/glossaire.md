# Glossaire : termes déjà acquis

Un terme est considéré comme acquis dès qu'il apparaît ici : ne plus le re-simplifier, l'utiliser directement.
Ce fichier grandit au fil des sessions. Celui-ci est un point de départ, à adapter à ton propre niveau.

- **API** : point d'entrée qu'un service expose pour qu'un autre outil vienne lui parler (comme un node HTTP Request dans n8n ou Make)
- **webhook** : URL qui reçoit un événement en temps réel et déclenche un workflow (le déclencheur « Webhook » dans n8n)
- **base de données** : là où sont stockées les données structurées (l'équivalent d'une base Airtable, mais côté Supabase / Postgres)
- **workflow** : l'automatisation elle-même, la suite d'étapes (n8n, Make)
- **node** : une étape, une brique dans un workflow n8n ou Make
- **trigger** : ce qui déclenche automatiquement une action (nouvelle ligne, webhook, cron)
- **cron** : programmation automatique répétée (tous les jours à telle heure, etc.)
- **migration** : un changement appliqué à la structure de la base de données (ajout de colonne, de règle, etc.)
- **appliquer une migration** : exécuter le fichier de migration sur la vraie base, pour que le changement décrit dedans existe pour de bon (le fichier seul, c'est un post-it « créer telle table » ; l'appliquer, c'est la créer)
- **RLS (Row Level Security)** : les règles qui filtrent qui a le droit de voir ou modifier quelle ligne dans une table Supabase
- **endpoint** : l'adresse précise à laquelle on appelle une API
- **branche (dans un workflow)** : un chemin alternatif à l'intérieur d'un workflow, une suite de nodes qui part sur un cas particulier (comme un IF qui ouvre deux chemins)
- **commit / push** : sauvegarder une version du code (commit) puis l'envoyer sur GitHub (push), et c'est souvent ce push qui déclenche le déploiement automatique en prod
- **branche (git)** : une copie parallèle de tout le projet sur laquelle on bricole sans toucher à la version officielle (`main`), comme dupliquer un workflow n8n en « test » pendant que l'original tourne en prod
- **merge** : reverser une branche dans la version officielle (`main`) une fois validée, ce qui envoie les modifs en prod
- **preview (Vercel)** : le site fabriqué automatiquement à partir d'une branche, avec sa propre URL de test, pendant que la vraie prod reste sur `main`
- **verrou** : une colonne de statut qui empêche qu'un même élément soit traité deux fois en même temps par deux exécutions d'un workflow qui se chevauchent
- **validation stricte (Zod)** : la vérification des données d'un formulaire avant de les enregistrer, pour rejeter ce qui ne correspond pas au format attendu
- **rate-limit** : une limite du nombre d'appels autorisés dans un temps donné, pour éviter qu'un bug ou un abus fasse exploser la facture d'une API
- **fail-closed** : quand une vérification échoue, on refuse au lieu de laisser passer (un garde-fou qui bloque en cas de doute plutôt que d'ouvrir en grand)
- **défense en profondeur** : ajouter une double vérification même si une protection existe déjà ailleurs, au cas où la première lâche
- **policy engine** : les règles de sécurité et les limites posées en dur dans le code (pas dans le prompt de l'IA), pour qu'elles tiennent même si l'IA se trompe
- **slice / couper la liste** : ne garder qu'une partie d'une liste de résultats (par exemple juste les éléments qui manquent pour atteindre un objectif)
- **tokens (design system)** : les réglages de base partagés (couleurs, polices, espacements) déclarés une seule fois pour que tous les écrans s'y réfèrent
- **composant (UI)** : une brique d'interface réutilisable (bouton, carte, badge) codée une seule fois, comme un sous-workflow n8n qu'on appelle au lieu de recopier les mêmes nodes
- **importer un package** : venir piocher du code publié ailleurs au lieu de le copier-coller, comme relier plusieurs bases Airtable à une source commune plutôt que dupliquer les données
- **prompt système** : les consignes permanentes envoyées à l'IA avant chaque question, que l'utilisateur final ne voit jamais (le cadre : de quoi elle a le droit de parler, ce qu'elle n'a pas le droit d'inventer)
- **encadrer par des balises** : entourer le texte d'un utilisateur de marqueurs comme `<message_client>` pour que l'IA le traite comme une question et jamais comme un ordre (même logique que ne pas faire confiance au contenu d'un webhook)
- **clé publique (Supabase)** : la clé d'accès à la base visible dans le code du site par n'importe quel visiteur ; seules les règles RLS décident ce qu'elle a le droit de lire ou modifier
- **fonction serveur (edge function)** : un petit programme hébergé chez Supabase qui fait le travail à la place du navigateur, comme un workflow n8n appelé par webhook qui vérifie un token avant d'écrire dans Airtable
- **compte de service (Google)** : une adresse mail de robot avec sa propre clé, à qui on partage un fichier Google comme à un collègue, exactement comme les identifiants Google d'un node n8n mais au nom du programme et pas d'un humain
- **variable d'environnement** : un réglage secret (mot de passe, clé, adresse) posé dans le tableau de bord de l'hébergeur au lieu d'être écrit dans le code, comme les credentials d'un node n8n
