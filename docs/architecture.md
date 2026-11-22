# Architecture cible — IA SYN EXPERT

## 1. Objectif
Créer un assistant documentaire privé pour les équipes SYN EXPERT, accessible via `ia.synexpert.fr`. La première version doit permettre de retrouver une procédure, poser une question et obtenir une réponse accompagnée de références vérifiables.

## 2. Périmètre du MVP
- Authentification obligatoire.
- Dépôt et gestion de documents avec métadonnées.
- Extraction du texte et indexation.
- Recherche hybride (texte + vecteurs) si elle apporte un gain mesuré.
- Réponse générée uniquement à partir des passages récupérés.
- Citations ouvrant le document et identifiant page/section lorsque disponibles.
- Gestion des erreurs, absence de source et feedback utilisateur.
- Administration simple des utilisateurs et des collections documentaires.

Hors périmètre initial : actions d'écriture dans Odoo, envoi d'e-mails, automatisations métier autonomes et accès public anonyme.

## 3. Architecture logique
- **Frontend** : application web responsive, interface de conversation, affichage des sources et espace d'administration.
- **API backend** : authentification, autorisations, ingestion, recherche, orchestration RAG et journalisation.
- **Stockage relationnel** : utilisateurs, rôles, documents, métadonnées, conversations et traces techniques minimales.
- **Stockage documentaire** : fichiers originaux dans un espace privé, jamais exposé directement.
- **Index de recherche** : index textuel et, après validation, index vectoriel.
- **Fournisseur IA** : appelé depuis le backend uniquement ; aucune clé exposée au navigateur.

Les technologies définitives doivent être choisies après inspection du dépôt et vérification de l'environnement de déploiement. Une piste raisonnable à évaluer : Next.js pour l'interface, FastAPI pour l'API, PostgreSQL avec extension vectorielle si nécessaire, et stockage objet privé.

## 4. Sécurité et confidentialité
- Authentification et autorisation vérifiées côté serveur.
- Cloisonnement des documents par organisation/équipe et niveau d'accès.
- Chiffrement en transit et au repos selon les capacités de l'hébergement.
- Secrets fournis par variables d'environnement ou coffre de secrets.
- Limitation de taille et contrôle des types de fichiers importés.
- Protection contre les injections de prompt dans les documents.
- Journalisation sans contenu documentaire sensible ni secrets.
- Politique de conservation, export et suppression à définir avant production.
- Aucune donnée réelle de client dans les jeux de tests.

## 5. Connecteurs Odoo — phase ultérieure
Prévoir trois connecteurs indépendants :
- Odoo SYN EXPERT France ;
- Odoo SYN EXPERT Maroc ;
- Odoo FretZen.

Chaque connecteur doit avoir ses propres paramètres et identifiants, être désactivable indépendamment et appliquer une liste blanche de modèles/champs. Mode lecture seule exclusivement au départ. Aucun accès production avant revue de sécurité et autorisation explicite.

## 6. Environnements
- Local : données fictives et services isolés.
- Test : jeux de données synthétiques.
- Préproduction : configuration proche de la production, sans données réelles non nécessaires.
- Production : déploiement séparé, secrets gérés hors Git, sauvegardes et supervision.

## 7. Découpage proposé
1. Audit du dépôt et choix d'architecture.
2. Squelette applicatif, configuration locale et CI.
3. Authentification et rôles.
4. Ingestion documentaire et stockage privé.
5. Recherche et réponses sourcées.
6. Tests de sécurité, observabilité et recette.
7. Déploiement contrôlé sur le domaine cible.
8. Connecteurs Odoo en lecture seule.

## 8. Décisions à confirmer
- Hébergement et contraintes d'infrastructure.
- Fournisseur de modèle et localisation/traitement des données.
- Système d'identité et politique de rôles.
- Types de documents et volumes attendus.
- Politique de conservation et niveaux de confidentialité.
