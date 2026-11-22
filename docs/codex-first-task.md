# Première tâche Codex — audit et socle du MVP

Vous travaillez dans le dépôt `synexpert/IA-synexpert`.

## Étape 1 — Audit
- Inspecter tous les fichiers et l'historique utile.
- Identifier les technologies déjà présentes, leur état, les commandes disponibles et les éventuels tests.
- Ne pas remplacer une architecture existante sans argument.
- Signaler les informations manquantes plutôt que les inventer.

## Étape 2 — Proposition
Présenter un plan d'implémentation court couvrant :
- architecture frontend/backend ;
- authentification et rôles ;
- stockage privé des documents ;
- ingestion et recherche ;
- citations et traçabilité ;
- tests et CI ;
- exécution locale.

## Étape 3 — Implémentation initiale
Après l'audit, créer le plus petit socle exécutable cohérent avec l'existant :
- structure de code claire ;
- configuration locale documentée ;
- `.env.example` sans secret ;
- endpoint de santé ;
- interface d'accueil sobre indiquant le périmètre de l'assistant ;
- tests minimaux et CI si le dépôt s'y prête.

Ne pas construire un RAG fictif ni prétendre qu'un connecteur fonctionne sans intégration testée.

## Étape 4 — Contrôles
- Installer les dépendances de manière reproductible.
- Exécuter les tests, lint et build disponibles.
- Corriger les erreurs introduites.
- Documenter précisément ce qui a été exécuté et ce qui reste à faire.

## Contraintes
- Ne pas déployer.
- Ne pas contacter les environnements Odoo.
- Ne pas demander ni ajouter de secrets.
- Ne pas fusionner la branche principale.
- Ouvrir une pull request de proposition avec résumé, tests, limites et captures d'écran si une interface est créée.
