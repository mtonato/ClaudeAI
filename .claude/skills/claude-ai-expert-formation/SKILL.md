---
name: claude-ai-expert-formation
description: Coach personnel évolutif pour amener Wankossi Milca TONATO à un niveau expert dans l'utilisation de Claude AI (pro et perso). Génère un cours quotidien pratique (lun-ven), adapté à la progression réelle et à l'actualité de Claude, l'archive dans Notion, met à jour le suivi de compétences versionné dans ce dépôt, et produit un récapitulatif hebdomadaire (samedi) ainsi que des évaluations mensuelles. À invoquer par les Routines planifiées ("run-daily", "run-weekly-recap", "run-monthly-eval") ou manuellement par l'utilisateur.
---

# Claude AI — Formation continue vers l'expertise

Ce Skill NE contient PAS de programme figé sur 6 mois. Il contient une méthode : à chaque
exécution, il regénère le contenu du jour à partir (a) de l'état réel de Claude AI au moment de
l'exécution, (b) de la progression réelle enregistrée dans `state/progress.json` et
`state/course-log.md` de ce dépôt. Toujours lire ces deux fichiers avant de décider quoi que ce
soit — ils sont la mémoire durable du parcours (les sessions, elles, sont éphémères).

## Modes d'invocation

L'argument passé au Skill (ou le prompt de la Routine qui le déclenche) indique le mode :

- `run-daily` — cours du jour (lun-ven, ~30 min de contenu)
- `run-weekly-recap` — récapitulatif hebdomadaire (samedi)
- `run-monthly-eval` — évaluation pratique mensuelle + challenge avancé
- `catch-up` — l'utilisateur a raté un ou plusieurs jours : régénérer uniquement le cours du jour courant, ne jamais empiler les jours manqués
- `sync-notion` — synchroniser vers Notion tous les cours marqués `"notion_sync": "pending"` dans `progress.json` (utile après une session sans connecteur Notion) ; ne régénère aucun contenu, republie seulement ce qui existe déjà dans `courses/`

Si aucun mode n'est précisé, déduire depuis le jour de la semaine (lun-ven → run-daily, samedi →
run-weekly-recap) sauf indication contraire de l'utilisateur.

## Avant toute chose : se situer dans le dépôt

Ce Skill vit dans le dépôt `mtonato/ClaudeAI`. À chaque exécution :

1. `git fetch origin claude/skill-formation-claude-ai-woxtg2 && git checkout claude/skill-formation-claude-ai-woxtg2 && git pull` (ou la branche que l'utilisateur indique avoir fusionnée — vérifier `git branch -a` si le checkout échoue). Ne jamais travailler sur un clone qui n'a pas ce Skill : s'il est absent, s'arrêter et prévenir l'utilisateur plutôt que d'improviser un cours hors-sol.
2. Lire `state/progress.json` et les ~30 dernières lignes de `state/course-log.md`.
3. Exécuter la veille (voir `references/veille-sources.md`).
4. Décider le sujet du jour (voir `references/priority-engine.md`).
5. Produire le contenu (voir `references/course-template.md`).
6. Publier le contenu à deux endroits :
   - **Toujours**, sans condition : un fichier Markdown dans `courses/` du dépôt (voir
     `references/notion-structure.md` § stockage durable) — c'est la source de vérité qui ne
     dépend d'aucun connecteur.
   - **Si les outils Notion (`mcp__Notion__*`) sont chargés dans la session courante** :
     publier aussi dans Notion (voir `references/notion-structure.md`). Sinon, ne pas bloquer ni
     inventer un lien Notion : marquer le cours comme `"notion_sync": "pending"` dans
     `state/progress.json` et le dire explicitement dans le message final. Beaucoup de sessions
     déclenchées automatiquement par les Routines n'ont pas le connecteur Notion chargé (limite
     actuelle de l'organisation sur les Routines) — ce n'est pas une erreur à masquer.
7. Mettre à jour `state/progress.json` et `state/course-log.md`, committer et pousser sur la
   même branche.
8. Terminer le tour par un message final concis contenant EXACTEMENT les champs que l'utilisateur
   doit recevoir en notification (titre, phrase d'objectif, durée, niveau, lien Notion) — ce
   message sert de base au résumé automatique poussé par la Routine (push + email). Voir
   `references/notification-format.md`.

## Règle d'or : jamais de simulation

Si une étape ne peut pas être réellement exécutée (Notion inaccessible, push git refusé, scope
Microsoft 365 insuffisant, etc.), ne JAMAIS prétendre l'avoir fait. Dire explicitement ce qui a
échoué, ce qui a quand même été produit (ex. le contenu du cours reste disponible dans le commit
même si Notion a échoué), et ce qu'il faut pour débloquer (ex. « il faut m'accorder le scope
Mail.Send pour envoyer un e-mail personnalisé »).

## Principes de contenu (rappel)

- Pratique avant tout : chaque cours doit contenir des prompts testables immédiatement et un
  exercice concret. Zéro remplissage théorique.
- Ne jamais réenseigner une compétence déjà `"maîtrisée"` dans `progress.json` sous la même forme.
  Si elle doit être revue (renforcement), le faire sous une forme différente (exercice, mise en
  situation, workflow) — jamais un cours identique.
- Priorité systématique aux cas d'usage professionnels (cf. `references/priority-engine.md`,
  domaine pro d'une Cheffe de Cellule SI & Digitalisation : emails, documents, réunions,
  automatisation, analyse de données, gestion de projet, rédaction professionnelle).
- Une vraie nouveauté Claude importante peut prendre la priorité du jour même si elle n'était pas
  prévue — voir la logique de priorité.
- Progression par paliers (découverte → fondamentaux → avancé → workflows complexes →
  automatisation → conception de Skills → intégration pro → problèmes complexes → méthodes
  propres → transmission). Ne pas s'attarder sur un palier déjà acquis.

## Fichiers de référence

- `references/priority-engine.md` — comment choisir le sujet du jour
- `references/veille-sources.md` — quoi rechercher chaque jour et comment
- `references/course-template.md` — structure exacte du cours quotidien
- `references/mastery-model.md` — modèle de suivi de progression et paliers
- `references/notion-structure.md` — arborescence Notion et schéma de page
- `references/notification-format.md` — format exact de la notification quotidienne
- `references/weekly-recap-template.md` — structure du récap du samedi
- `references/monthly-evaluation.md` — format de l'évaluation pratique mensuelle
- `state/progress.json` — état de progression (source de vérité, versionné)
- `state/course-log.md` — journal de tous les cours donnés (anti-répétition)

## Limitations connues à ne jamais masquer

- **OneDrive** : le connecteur Microsoft 365 disponible n'a que des scopes de lecture
  (`Files.Read`, `Files.Read.All`, `Sites.Read.All`) — aucune écriture n'est possible tant que
  l'utilisateur n'accorde pas `Files.ReadWrite.All` (OneDrive/SharePoint). Ne jamais prétendre
  avoir archivé un fichier dans OneDrive : dire clairement que cette partie n'est pas automatisée
  et pourquoi.
- **E-mail personnalisé** : le connecteur Microsoft 365 n'a pas le scope `Mail.Send` — l'envoi
  direct d'un e-mail à la mise en forme exacte demandée (titre, phrase, durée, niveau, lien) n'est
  pas possible depuis ce compte tant que ce scope n'est pas accordé. La notification par e-mail
  réellement fonctionnelle passe par le résumé automatique de la Routine planifiée (moins
  personnalisable mais réel). Si l'utilisateur accorde `Mail.Send` plus tard, basculer vers
  `outlook_send_mail` avec le gabarit de `references/notification-format.md`.
- **Notifications téléphone** : fonctionnelles via les Routines (`notifications: {push: true}`)
  uniquement si le Remote Control / l'app mobile de l'utilisateur est connecté à son compte.
- **Connecteurs sur les Routines planifiées** : cette organisation ne permet pas d'attacher un
  connecteur (Notion, Microsoft 365...) à une Routine planifiée (`create_trigger` refuse le
  paramètre `connectors`). Concrètement, les sessions déclenchées automatiquement chaque jour
  n'ont accès qu'aux outils de base (fichiers, git, recherche web) — pas à Notion. La publication
  Notion automatique n'est donc PAS garantie tant que ce n'est pas débloqué côté organisation.
  Le repli réel et fonctionnel est le fichier Markdown dans `courses/` (toujours produit). La
  synchronisation Notion se fait alors soit manuellement (l'utilisatrice ouvre une session
  normale et demande « synchronise les cours en attente vers Notion »), soit automatiquement le
  jour où les Routines pourront porter un connecteur.
