# Appunti Git

Appunti di studio su Git, da zero ad avanzato. Pensati come percorso ordinato
ma usabili anche come reference rapida durante il lavoro.

## Come sono organizzati

- File numerati per topic (`01-*.md`, `02-*.md`, ...) da leggere in ordine.
- Ogni file segue lo stesso scheletro (vedi [REGOLE.md](REGOLE.md)).
- Termini tecnici e comandi restano in inglese; il testo è in italiano semplice.

## Indice topic

> La sequenza viene definita man mano, in base al materiale.

| # | File | Argomento |
|---|------|-----------|
| — | —    | (da popolare) |

## File di supporto

- [REGOLE.md](REGOLE.md) — le regole di qualità che ogni appunto deve rispettare.
- [glossario.md](glossario.md) — termini Git (EN) spiegati in italiano semplice.
- [playbook.md](playbook.md) — ricette pronte: problema reale → comandi esatti.

## Convenzioni

- Commit in stile [Conventional Commits](https://www.conventionalcommits.org/)
  (`docs:`, `fix:`, ...).
- Comandi pericolosi marcati con ⚠️.

## Anteprima locale

Il sito è generato con [Docsify](https://docsify.js.org/) (nessuna build).
Per vederlo in locale serve un server statico (non basta aprire il file):

```bash
npx serve .          # poi aprire l'indirizzo mostrato
# oppure
python3 -m http.server
```
