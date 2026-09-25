---
name: Nouvelle feature
about: Démarrer un chantier en listant d'abord les tests à écrire
title: "[Feature] "
labels: feature
---

## Ce que la feature doit faire

<!-- En une ou deux phrases, du point de vue de l'utilisateur. -->

## Comportements attendus

<!-- Un comportement par ligne. Chacun deviendra au moins un test. -->

- [ ] ...
- [ ] ...

## Plan de tests (à remplir AVANT de coder)

### Tests unitaires
<!-- Une petite brique isolée, sans base de données ni réseau. Rapides, nombreux. -->

- [ ] ...

### Tests d'intégration
<!-- Deux ou trois briques ensemble : code + base de données, code + stockage... -->

- [ ] ...

### Tests end-to-end
<!-- Le parcours complet comme un vrai utilisateur. Seulement les parcours critiques. -->

- [ ] ...

## Ordre de travail

1. Écrire le premier test unitaire, le voir rouge.
2. Coder le minimum pour le passer au vert, puis nettoyer.
3. Recommencer pour chaque comportement de la liste.
4. Ajouter les tests d'intégration une fois les briques prêtes.
5. Finir par le ou les tests end-to-end du parcours.
