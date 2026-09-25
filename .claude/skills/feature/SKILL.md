---
name: feature
description: Démarre une nouvelle feature du projet video-hosting en test first. Rédige le plan de tests (unitaires, intégration, end-to-end), le fait valider, crée l'issue GitHub, puis déroule le cycle rouge-vert-refactor jusqu'à la PR. À utiliser dès qu'on commence une feature, un chantier ou une fonctionnalité nouvelle, ou quand l'utilisateur tape /feature.
---

# Démarrer une feature en test first

Ce skill applique les règles de `CLAUDE.md` et de `docs/TDD.md`. En cas de doute, ces deux fichiers font foi.

## Étape 1 : comprendre la feature

Pars de la description donnée par l'utilisateur après `/feature`. Si elle manque, demande-la en une question courte.
Reformule la feature en une ou deux phrases, du point de vue de l'utilisateur final.

## Étape 2 : écrire le plan de tests

Liste les comportements attendus, un par ligne, formulés comme des phrases observables
(par exemple « rejette une vidéo de plus de 2 Go »).

Range chaque comportement dans un niveau de test :

- **Unitaire** : une règle métier isolée, sans base de données, réseau ni disque. C'est le niveau par défaut.
- **Intégration** : plusieurs briques ensemble, par exemple le code et la base de données, ou le code et le stockage.
- **End-to-end** : le parcours complet d'un utilisateur. Réserve-le aux parcours critiques, un ou deux par feature.

Pense aussi aux cas d'erreur et aux limites : fichier vide, taille maximale, droits d'accès, état inattendu.

## Étape 3 : faire valider le plan

Montre le plan à l'utilisateur sous forme de liste et attends sa validation avant d'écrire du code.
Intègre ses corrections.

## Étape 4 : créer l'issue GitHub

Crée une issue dans le dépôt en reprenant la structure de `.github/ISSUE_TEMPLATE/feature.md` :
description, comportements attendus, plan de tests par niveau, ordre de travail.
Donne le lien de l'issue à l'utilisateur.

## Étape 5 : dérouler le cycle rouge-vert-refactor

Pour chaque comportement, dans cet ordre : unitaires, puis intégration, puis end-to-end.

1. **Rouge** : écris un seul test, lance-le, vérifie qu'il échoue sur l'assertion attendue.
2. **Vert** : écris le code minimal qui le fait passer, puis relance toute la suite.
3. **Refactor** : nettoie le code et le test, la suite doit rester verte.
4. Commite le test et son code ensemble, puis coche le comportement dans l'issue.

Utilise les commandes de test de la section « Commandes de test » de `CLAUDE.md`.
Si elles sont encore « à définir », la stack n'est pas choisie : arrête-toi après l'étape 4
et explique à l'utilisateur qu'il faut d'abord installer la stack et son lanceur de tests.

Règles à ne jamais enfreindre : pas de code sans test rouge d'abord, aucun test skippé,
désactivé ou supprimé pour passer au vert.

## Étape 6 : ouvrir la PR

Lance la suite complète une dernière fois. Ouvre la PR en remplissant le template
`.github/pull_request_template.md`, avec le plan de tests coché et un lien vers l'issue.

Ne programme aucune surveillance automatique de la PR sauf si l'utilisateur le demande.
