# Checklist OWASP Top 10:2025

Source : https://top10.owasp.org/2025/

## Quand la repasser
- Avant chaque mise en production
- Dès qu'on touche à l'authentification, aux permissions ou aux données utilisateurs
- Dès qu'on ajoute une dépendance ou un service externe

Une ligne qui n'est pas cochée n'est pas un détail à traiter plus tard : c'est une décision à prendre et à écrire.

## Les 10 points

- [ ] **A01 Broken Access Control** : un compte connecté peut-il lire ou modifier les données d'un autre compte ? Tester en conditions réelles avec deux comptes, pas en lisant le code. *Cas typique : une table sans règle d'écriture qui reste ouverte des jours sans que personne ne le voie.*
- [ ] **A02 Security Misconfiguration** : `.env` bien ignoré par git, aucune clé de service côté client, pas de compte ni de mot de passe par défaut laissé actif.
- [ ] **A03 Software Supply Chain Failures** : d'où viennent les dépendances et les templates utilisés, et qui peut pousser du code qui part en production ?
- [ ] **A04 Cryptographic Failures** : quelles données sensibles sont stockées, et sous quelle forme ? Aucun secret, aucun code d'accès en clair dans le dépôt ni dans un document qui circule (captures d'écran et documentation comprises).
- [ ] **A05 Injection** : toute entrée utilisateur est validée côté serveur, jamais concaténée dans une requête. Vaut aussi pour les entrées passées à un modèle IA.
- [ ] **A06 Insecure Design** : le scénario d'abus a-t-il été posé avant de coder ? Qui a intérêt à tricher ici, et qu'est-ce qui l'en empêche ?
- [ ] **A07 Authentication Failures** : comment on se connecte, comment on se déconnecte partout, et que vaut réellement le facteur utilisé (un code à 4 chiffres n'est pas une authentification).
- [ ] **A08 Software or Data Integrity Failures** : que se passe-t-il si une automatisation écrase une donnée saisie à la main ? Qui gagne en cas de conflit, et c'est écrit où ?
- [ ] **A09 Security Logging and Alerting Failures** : si ça tombe en panne cette nuit, qui l'apprend et au bout de combien de temps ? Une alerte que personne n'ouvre ne compte pas comme une alerte. *Cas typique : des relances automatiques en panne une semaine sans aucun signal.*
- [ ] **A10 Mishandling of Exceptional Conditions** : que fait le système quand l'API externe ne répond pas, renvoie une erreur ou des données vides ? Un échec silencieux est pire qu'un plantage.

## Règle
Les points non traités restent listés ici avec la raison et la date, jamais effacés.
