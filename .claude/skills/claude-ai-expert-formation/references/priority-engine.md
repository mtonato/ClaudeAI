# Moteur de priorité du sujet du jour

À chaque exécution `run-daily`, évaluer dans cet ordre et retenir le premier critère qui matche
avec un sujet concret et justifié. Ne jamais choisir un sujet par défaut/aléatoire — toujours
pouvoir justifier le choix en une phrase dans le cours (section « Pourquoi aujourd'hui »).

1. **Nouveauté Claude importante** (détectée par la veille du jour, cf. `veille-sources.md`) qui
   change réellement une façon de travailler (nouvelle fonctionnalité, nouveau modèle, nouvelle
   capacité d'outil, changement de comportement notable). Une nouveauté mineure ou cosmétique ne
   déclenche pas ce niveau.
2. **Fonctionnalité à fort potentiel de gain pro** identifiée mais jamais pratiquée par
   l'utilisatrice (croiser `progress.json.underused_features`) — en particulier tout ce qui touche
   Projects, Skills, Artifacts, connecteurs, gestion de fichiers, automatisation, workflows
   multi-étapes.
3. **Compétence manquante** identifiée dans `progress.json.fragile_skills` ou dans les résultats
   de la dernière évaluation mensuelle.
4. **Approfondissement** d'une compétence importante déjà entamée mais pas encore au niveau
   « avancé » dans `progress.json.mastered_skills`.
5. **Cas d'usage professionnel pertinent** non encore couvert, tiré de la liste métier (emails,
   documents, réunions, comptes rendus, rédaction, analyse/synthèse, présentations, veille,
   gestion de projet, automatisation, analyse de données, workflows, conception de Skills,
   connecteurs, fichiers, Artifacts, développement).
6. **Technique ou astuce avancée** de prompting/méthode Claude, quand rien de plus prioritaire
   n'est disponible.

## Anti-répétition

Avant de valider un sujet, vérifier `state/course-log.md` :
- Si le même sujet exact a déjà été couvert et est marqué `"mastered"` dans `progress.json`, ne
  pas le reprendre sous la même forme. Un retour dessus doit changer de format (exercice avancé,
  mise en situation, intégration dans un workflow plus large).
- Ne jamais présenter comme nouvelle une fonctionnalité déjà enseignée il y a moins de
  ~6 semaines sans qu'un changement réel la justifie.

## Paliers de progression (voir aussi mastery-model.md)

Ne pas revenir en arrière dans les paliers sauf lacune identifiée. Une fois qu'un palier est
raisonnablement couvert (plusieurs compétences clés en `mastered`), orienter les prochains choix
vers le palier suivant.
