# Playbook

Ricette pronte per problemi reali di lavoro. Ogni voce: problema in linguaggio
naturale → comandi esatti → nota safe/destructive. Per la teoria, seguire i link
ai file topic.

## Formato di una ricetta

```markdown
### <Problema in una frase>

\`\`\`bash
<comandi esatti>
\`\`\`

- Nota: safe / ⚠️ destructive + cosa cambia.
- Approfondimento: [link al topic].
```

---

## Ricette

### Ho committato e pushato, devo annullare quel commit

```bash
git revert <hash>      # crea un nuovo commit che annulla le modifiche
git push               # pubblica l'annullamento
```

- Nota: **safe**. Non riscrive la storia: aggiunge un commit "inverso", quindi
  è l'opzione corretta quando il commit è già stato pushato e condiviso.
- Evitare `git reset` su commit già pushati ⚠️ (riscrive la storia condivisa).
- Approfondimento: (topic "Annullare", da scrivere).
