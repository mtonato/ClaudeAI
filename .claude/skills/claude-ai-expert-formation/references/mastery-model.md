# Modèle de suivi de progression

Source de vérité : `state/progress.json`. Toujours le lire avant de décider un sujet, toujours le
mettre à jour après un cours, un récap ou une évaluation.

## Paliers (non calendaires, on avance quand c'est mérité)

1. `decouverte`
2. `fondamentaux`
3. `avance`
4. `workflows-complexes`
5. `automatisation`
6. `conception-skills`
7. `integration-pro`
8. `resolution-problemes-complexes`
9. `methodes-propres`
10. `transmission`

## Statut d'une compétence

Chaque compétence (tag court, ex. `prompting-avance`, `artifacts`, `connecteurs`, `projects`,
`skills-design`, `workflows`) a un statut :

- `introduite` — vue une fois, pas encore pratiquée sérieusement
- `en-cours` — pratiquée au moins une fois avec exercice réussi
- `fragile` — pratiquée mais résultat incertain / erreurs répétées / évitée par l'utilisatrice
- `mastered` — démontrée de façon autonome (exercice réussi + réutilisée spontanément plus tard)

## Règles de mise à jour après chaque cours

1. Ajouter/mettre à jour les compétences travaillées avec leur nouveau statut (ne jamais rétrograder
   sans raison : seulement en cas d'échec net à un exercice ou une évaluation).
2. Ajouter le sujet à `underused_features` s'il révèle qu'une fonctionnalité connue est peu
   utilisée (ex: l'utilisatrice ne s'est jamais servie des Projects).
3. Mettre à jour `current_track` (le palier en cours) si un palier semble globalement acquis
   (majorité de ses compétences clés en `mastered`).
4. Ajouter le sujet, la date, le lien Notion et le niveau à l'historique.

## Évaluation mensuelle → mise à jour de masse

Après `run-monthly-eval`, réviser les statuts en bloc à partir des résultats réels (pas
déclaratifs) : ce qui a été démontré en situation passe `mastered`; ce qui a échoué ou a été évité
passe/reste `fragile`.
