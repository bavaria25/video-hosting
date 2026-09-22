# Test first / TDD sur video-hosting

Ce document est le pense-bête de la méthode. La règle courte est dans
`CLAUDE.md` ; ici on détaille le pourquoi et le comment.

## Le cycle

```
   ┌──────────┐     ┌──────────┐     ┌────────────┐
   │  ROUGE   │ ──▶ │   VERT   │ ──▶ │  REFACTOR  │ ──┐
   │ test qui │     │ code     │     │ nettoyer,  │   │
   │ échoue   │     │ minimal  │     │ suite verte│   │
   └──────────┘     └──────────┘     └────────────┘   │
        ▲                                             │
        └─────────────────────────────────────────────┘
```

### Rouge

- Écrire **un seul** test, pour **un seul** comportement.
- Le lancer. Vérifier qu'il échoue, et qu'il échoue sur l'assertion attendue.
  Un test qui échoue parce que la fonction n'existe pas encore est acceptable,
  mais l'étape suivante consiste alors à créer la fonction vide et à relancer
  pour obtenir l'échec d'assertion.
- Si le test passe du premier coup, soit le comportement existe déjà, soit le
  test ne teste rien. Dans les deux cas, ne pas continuer sans comprendre.

### Vert

- Écrire le code le plus simple qui fait passer le test, même s'il paraît
  bête (retourner une constante est autorisé à ce stade).
- Ne pas anticiper les cas suivants. Ils auront leur propre test.
- Relancer la suite complète, pas seulement le nouveau test.

### Refactor

- Supprimer la duplication, renommer, extraire. Dans le code **et** dans les
  tests.
- Ne changer aucun comportement : si un test casse pendant le refactor, on
  revient en arrière.
- Commiter à la fin du cycle.

## Ce qu'on teste en priorité

Pour un service d'hébergement vidéo, les comportements à couvrir en premier
sont ceux qui coûtent cher quand ils cassent :

- Validation des uploads : taille, format, durée, nom de fichier.
- Règles d'accès : qui peut voir, modifier, supprimer une vidéo.
- Transitions d'état d'une vidéo : envoyée, en cours de traitement, prête,
  échec, supprimée.
- Génération d'URL de lecture et leur expiration.
- Quotas et limites par utilisateur.

Le stockage, le transcodage et les appels réseau sont derrière des interfaces
que les tests remplacent par des doubles. On ne teste pas S3 ni ffmpeg, on
teste que notre code les appelle correctement et réagit bien à leurs réponses.

## Pièges à éviter

- **Écrire plusieurs tests avant le premier vert.** On perd le signal de ce qui
  casse et pourquoi.
- **Tester l'implémentation.** Un test qui vérifie qu'une méthode privée est
  appelée casse à chaque refactor sans protéger de rien.
- **Mocker ce qu'on possède.** Si le code est à nous, on le teste pour de vrai.
  On ne double que les frontières : réseau, disque, temps, aléatoire.
- **Passer au vert en désactivant le test.** Interdit. Un test rouge est une
  information, pas un obstacle.
- **Commiter le code sans son test.** Le test fait partie du changement.

## Quand la stack sera choisie

Le premier commit de stack doit contenir :

1. Le lanceur de tests installé et configuré.
2. Un test trivial qui passe (par exemple `1 + 1 == 2`), pour prouver que la
   chaîne fonctionne.
3. Les commandes réelles reportées dans le tableau de `CLAUDE.md`.
4. Un job CI qui lance la suite sur chaque push et chaque PR.

À partir de là, chaque fonctionnalité commence par un test rouge.
