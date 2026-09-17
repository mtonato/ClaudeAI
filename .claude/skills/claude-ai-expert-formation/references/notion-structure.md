# Structure Notion — « Claude AI — Parcours Expert »

Espace dédié à ce parcours personnel, distinct de tout autre programme existant dans le workspace
(ex. ne pas mélanger avec « Programme Claude IA – Équipe SI & Digitalisation », qui est un
programme d'équipe séparé).

Page racine : **Claude AI — Parcours Expert** (page privée, créée en mode draft si aucune
destination n'est précisée par l'utilisatrice), avec sous-pages :

- 📚 **Cours quotidiens** — une page par cours, propriétés minimales : date, titre, niveau,
  compétences travaillées, nouveauté Claude traitée (oui/non). Contenu : objectif, explication,
  exemples, prompts, exercice, défi, pièges, astuce, ressources (cf. `course-template.md`).
- 📊 **Progression** — reflet lisible de `state/progress.json` + comptes rendus d'évaluations
  mensuelles.
- 🏆 **Compétences acquises** — liste vivante des compétences `mastered`.
- 💡 **Astuces et bonnes pratiques** — capitalisation transverse (pas dupliquée depuis chaque
  cours, uniquement ce qui mérite d'être réutilisé tel quel).
- 🆕 **Nouveautés Claude** — une entrée par nouveauté traitée (date, changement, intérêt, usage).
- 🧪 **Exercices et challenges** — exercices marquants + évaluations mensuelles + défis avancés.
- 📅 **Récapitulatifs hebdomadaires** — un récap par semaine (cf. `weekly-recap-template.md`).

## Stockage durable indépendant de Notion

Chaque cours, récap ou évaluation est d'abord écrit dans `courses/AAAA-MM-JJ-slug.md` (dépôt
`mtonato/ClaudeAI`), quel que soit le succès de la publication Notion. C'est la source de vérité
qui ne dépend d'aucun connecteur — utile en particulier pour les sessions déclenchées par les
Routines planifiées, qui n'ont pas accès au connecteur Notion dans cette organisation (voir
SKILL.md § Limitations connues). La notification du jour peut donc pointer vers ce fichier
(lien GitHub) quand la publication Notion n'a pas pu avoir lieu.

## Notes d'implémentation

- Utiliser l'outil de création de pages Notion pour chaque nouvel élément ; toujours vérifier au
  préalable si la page racine existe déjà (recherche par titre) avant d'en recréer une.
- Le lien de chaque page créée doit être récupéré et réutilisé (notification du jour, récap
  hebdo).
- En cas d'échec d'accès à Notion, ne jamais simuler la création : suivre la règle d'or du
  `SKILL.md`.
