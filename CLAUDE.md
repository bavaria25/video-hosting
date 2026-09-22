# video-hosting — règles de développement

## Test first / TDD (obligatoire)

Tout le code de ce projet est écrit en **test first**. Aucune exception, y compris
pour les sessions Claude Code.

Cycle à suivre pour chaque changement de comportement :

1. **Rouge** — écrire un test qui décrit le comportement attendu et le lancer.
   Il doit échouer pour la bonne raison (pas une erreur de syntaxe ou d'import).
2. **Vert** — écrire le code minimal qui fait passer ce test. Rien de plus.
3. **Refactor** — nettoyer le code et les tests, la suite restant verte.
4. Recommencer avec le prochain comportement.

Règles concrètes :

- Pas de code de production sans test qui échoue d'abord. Un bug se corrige en
  écrivant d'abord le test qui le reproduit.
- Un commit = un cycle ou un petit groupe de cycles cohérents. Le test et le
  code qu'il couvre arrivent dans le même commit (ou le test dans le commit
  précédent), jamais le code seul.
- Ne jamais skipper, désactiver ou supprimer un test pour passer au vert.
- Les tests décrivent un comportement observable, pas une implémentation :
  nommer les tests par ce qu'ils vérifient (`rejette une vidéo de plus de 2 Go`),
  pas par la méthode appelée.
- Avant d'ouvrir ou de mettre à jour une PR, lancer la suite complète et
  cocher la checklist du template de PR.

Le détail du cycle et des pièges habituels est dans `docs/TDD.md`.

## Commandes de test

La stack n'est pas encore choisie. Dès qu'elle l'est, renseigner ici les
commandes réelles et remplacer ce paragraphe :

| Action                         | Commande |
| ------------------------------ | -------- |
| Lancer toute la suite          | à définir |
| Lancer un seul fichier de test | à définir |
| Mode watch pendant le cycle    | à définir |

Le premier commit qui introduit la stack doit aussi introduire le lanceur de
tests et un premier test qui passe, afin que le cycle rouge-vert soit
possible dès la fonctionnalité suivante.
