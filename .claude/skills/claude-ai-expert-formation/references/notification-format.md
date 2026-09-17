# Format de la notification quotidienne

Le dernier message texte de la session déclenchée par la Routine doit reproduire EXACTEMENT ce
gabarit (c'est ce message qui sert de base au résumé automatique push/email de la Routine) :

```
🎓 Claude AI — Cours du jour
Sujet : <titre du cours>
Durée : ~30 min
Niveau : <Débutant|Intermédiaire|Avancé|Expert>
Aujourd'hui, tu vas apprendre à <objectif en une phrase>.
👉 Accéder au cours : <lien Notion de la page du jour>
```

Si Notion a échoué, remplacer la dernière ligne par une explication honnête (ne jamais inventer de
lien) :

```
⚠️ Le cours a été généré mais n'a pas pu être publié dans Notion : <raison>. Contenu disponible
dans le commit <sha court> du dépôt mtonato/ClaudeAI.
```

## Limitation actuelle (à rappeler si l'utilisatrice demande pourquoi l'e-mail n'est pas
personnalisé de la même façon)

Le compte Microsoft 365 connecté n'a pas le scope `Mail.Send` : impossible d'envoyer un e-mail
avec cette mise en forme exacte via Outlook depuis ce Skill. Le canal e-mail réellement actif est
le résumé automatique de la Routine planifiée, dérivé de ce même message. Si `Mail.Send` est
accordé un jour, utiliser `outlook_send_mail` avec ce gabarit en `bodyType: "html"`.
