# État réel de l'automatisation — Parcours Claude AI

Ce document dit précisément ce qui tourne vraiment aujourd'hui, ce qui est manuel, et pourquoi —
conformément à la consigne : pas d'automatisation fictive.

## 1. Ce qui est réellement automatisé

### Routines planifiées (Claude Code Remote)
Trois Routines créées sur le compte, dans l'environnement `env_017bSphGAMCMSUXShMi51CPG` :

| Routine | Horaire (heure locale Bénin, WAT = UTC+1) | Cron (UTC) | ID |
|---|---|---|---|
| Cours quotidien | Lun-Ven 07:45 | `45 6 * * 1-5` | `trig_01XMcaYohC9Xhvyc2CEixQEe` |
| Récap hebdomadaire | Samedi 09:00 | `0 8 * * 6` | `trig_01XxyAwh7pDX7ajxR3zr4jxD` |
| Vérification évaluation mensuelle | 1er et 15 du mois, 07:30 | `30 6 1,15 * *` | `trig_015oXjczc4nqGEMwveFoR5LY` |

Chaque déclenchement crée une **session fraîche** dans l'environnement, exécute le Skill
`claude-ai-expert-formation`, committe et pousse le résultat dans le dépôt, puis se termine par un
message qui sert de base à une notification automatique **push** (téléphone, si le Remote Control/
l'app est connecté au compte) et **e-mail** (résumé généré par la plateforme).

### Suivi de progression versionné
`state/progress.json` et `state/course-log.md` dans le dépôt sont la mémoire durable du parcours
(les sessions déclenchées sont éphémères, le dépôt git ne l'est pas). Chaque exécution les met à
jour et les pousse.

### Veille
Chaque exécution du cours quotidien fait une recherche web réelle avant de choisir le sujet (voir
`references/veille-sources.md`) — pas de simulation, pas de contenu figé.

### Archivage de secours (toujours actif)
Chaque cours/récap/évaluation est écrit dans `courses/AAAA-MM-JJ-*.md` du dépôt, **indépendamment**
de la disponibilité de Notion. C'est la vraie source de vérité.

## 2. Ce qui est partiellement automatisé (et pourquoi)

### Publication Notion
La structure Notion « Claude AI — Parcours Expert » a été créée (page racine + 7 sous-pages, liens
dans `state/progress.json`). **Mais** : cette organisation n'autorise pas d'attacher un connecteur
(Notion, Microsoft 365...) à une Routine planifiée — `create_trigger` a explicitement refusé le
paramètre `connectors`. Conséquence concrète : les sessions déclenchées automatiquement chaque
jour n'ont **pas** accès aux outils Notion. Le cours est donc bien produit et versionné dans le
dépôt (`courses/`), mais sa copie dans Notion ne se fait pas automatiquement tant que ce n'est pas
débloqué.

**Débloquer réellement cette limite (deux options)** :
1. Créer/activer la Routine correspondante depuis l'UI Claude.ai (chemin indiqué par l'outil :
   « ask the user to create it from claude.ai routines UI ») si cette interface permet d'attacher
   un connecteur à une Routine dans ce compte.
2. En attendant, lancer manuellement (une session normale, où le connecteur Notion est actif)
   la commande `sync-notion` du Skill pour republier tout ce qui est marqué
   `"notion_sync": "pending"` dans `progress.json` — par exemple une fois par semaine.

## 3. Ce qui n'est PAS automatisé, et pourquoi

### OneDrive
Le connecteur Microsoft 365 est connecté (compte `mtonato@adpme.bj`), mais les scopes accordés
sont **en lecture seule** : `Files.Read`, `Files.Read.All`, `Sites.Read.All` — pas de
`Files.ReadWrite.All`. Impossible techniquement d'écrire un fichier dans OneDrive/SharePoint avec
l'accès actuel. Aucune tentative d'écriture n'a été simulée.
**Pour débloquer** : accorder le scope `Files.ReadWrite.All` (OneDrive/SharePoint) au connecteur
Microsoft 365 dans les paramètres de connecteurs Claude — je pourrai alors créer l'arborescence
`Formation Claude AI/` demandée et y déposer chaque cours en DOCX/PDF/Markdown.

### E-mail personnalisé (mise en forme exacte demandée)
Le scope `Mail.Send` n'est pas accordé (seuls des scopes de lecture : `Mail.Read`,
`Mail.Read.Shared`, `Mail.ReadBasic`). Impossible d'envoyer un e-mail avec `outlook_send_mail`
depuis ce compte. Le canal e-mail réellement actif est le résumé automatique généré par la Routine
elle-même (moins personnalisable, mais réel et fonctionnel dès aujourd'hui).
**Pour débloquer** : accorder le scope `Mail.Send` au connecteur Microsoft 365 — je basculerai
alors sur un e-mail au gabarit exact demandé (`references/notification-format.md`).

### Notification téléphone
Fonctionne via le canal `push` des Routines, à condition que le Remote Control / l'application
mobile de l'utilisatrice soit connecté à son compte Claude. Rien à configurer côté Skill ; à
vérifier côté compte si aucune notification n'arrive.

## 4. Prochaine étape pour que tout tourne en continu

Ce Skill a été développé sur la branche `claude/skill-formation-claude-ai-woxtg2` du dépôt
`mtonato/ClaudeAI` (dépôt vide au départ, aucun autre historique). Les Routines ci-dessus checkout
explicitement cette branche à chaque déclenchement — elles fonctionnent donc déjà sans attendre une
fusion. Si cette branche est un jour fusionnée dans une branche par défaut, aucune action requise :
les prompts des Routines savent retrouver le Skill par son chemin de fichier en cas d'échec du
checkout direct.
