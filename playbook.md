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

- Nota: **safe**. Non riscrive la storia: aggiunge un commit "inverso", quindi è
  l'opzione corretta quando il commit è già stato pushato e condiviso.
- Evitare `git reset` su commit già pushati ⚠️ (riscrive la storia condivisa).
- Approfondimento: [Annullare](08-annullare.md).

### Ho committato ma NON ho ancora pushato, voglio disfare l'ultimo commit

```bash
git reset --soft HEAD~1     # annulla il commit, le modifiche restano pronte in staging
```

- Nota: **safe** (solo locale). `history` torna indietro di 1, working directory
  invariato. Con `--mixed` (default) le modifiche tornano non in staging.
- Approfondimento: [Annullare](08-annullare.md).

### Ho fatto reset --hard e ho perso un commit, lo voglio indietro

```bash
git reflog                 # trova il commit perso, es. HEAD@{1}
git reset --hard HEAD@{1}  # ⚠️ ripristina quello stato
```

- Nota: il reflog è **locale** e scade (~90 giorni). Funziona per errori recenti.
- Approfondimento: [Interni di Git](12-interni-git.md).

### Ho cancellato un branch per errore

```bash
git reflog                          # trova l'ultimo commit del branch, es. b2c1d3e
git branch nome-recuperato b2c1d3e  # ricrea il branch su quel commit
```

- Nota: **safe**. Funziona finché la voce è ancora nel reflog.
- Approfondimento: [Interni di Git](12-interni-git.md).

### Mi sono dimenticato un file nell'ultimo commit (non pushato)

```bash
git add file-dimenticato.txt
git commit --amend --no-edit   # aggiunge il file, tiene lo stesso messaggio
```

- Nota: ⚠️ riscrive l'ultimo commit. Solo se **non** ancora pushato.
- Approfondimento: [Commit](03-commit.md).

### Devo cambiare branch ma ho modifiche a metà

```bash
git stash            # mette da parte le modifiche
git switch altro     # lavora altrove
git switch -         # torna
git stash pop        # riprende le modifiche
```

- Nota: **safe**.
- Approfondimento: [Stash](09-stash.md).

### Un file già committato non doveva essere tracciato

```bash
echo "config.local" >> .gitignore
git rm --cached config.local   # toglie dal tracking, il file resta sul disco
git commit -m "chore: smette di tracciare config.local"
```

- Nota: **safe** (il file sul disco resta).
- Approfondimento: [.gitignore](05-gitignore.md).

### Aggiornare il mio feature branch con le ultime di main

```bash
git switch feature
git fetch
git rebase origin/main         # storia lineare
# se conflitti: risolvi i file, git add <file>, git rebase --continue
```

- Nota: ⚠️ se il branch è già condiviso con altri, valutare un `merge` invece del
  rebase (il rebase riscrive la storia).
- Approfondimento: [Rebase](10-rebase.md).

### Prima push di un branch nuovo

```bash
git push -u origin nome-branch   # imposta l'upstream; poi basta "git push"
```

- Nota: **safe**.
- Approfondimento: [GitHub](14-github.md).

### Voglio scartare modifiche non salvate / togliere un file dalla staging

```bash
git restore --staged file.txt    # toglie da staging, le modifiche restano
git restore file.txt             # ⚠️ scarta le modifiche non salvate (non recuperabili)
```

- Nota: `restore <file>` ⚠️ è distruttivo se le modifiche non erano in un commit.
- Approfondimento: [Annullare](08-annullare.md).
