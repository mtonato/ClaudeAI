# ClaudeAI — Parcours de formation continue

Ce dépôt héberge le Skill `claude-ai-expert-formation` : un coach personnel évolutif qui génère,
jour après jour, le contenu de formation de Wankossi Milca TONATO à l'utilisation experte de
Claude AI (pro et perso).

Le Skill ne contient pas de programme figé sur 6 mois : à chaque exécution, il regénère le sujet
du jour à partir de l'actualité réelle de Claude et de la progression réellement enregistrée. Voir
`.claude/skills/claude-ai-expert-formation/SKILL.md` pour le fonctionnement complet, et
`AUTOMATION.md` pour l'état réel de l'automatisation (ce qui tourne vraiment vs ce qui nécessite
une action manuelle).

## Structure

- `.claude/skills/claude-ai-expert-formation/SKILL.md` — instructions du Skill
- `.claude/skills/claude-ai-expert-formation/references/` — gabarits et règles (priorité, veille,
  cours, progression, Notion, notifications, récap, évaluation)
- `.claude/skills/claude-ai-expert-formation/state/progress.json` — état de progression
  (source de vérité, versionnée)
- `.claude/skills/claude-ai-expert-formation/state/course-log.md` — journal de tous les cours
- `AUTOMATION.md` — routines planifiées, capacités réelles, limitations
