# Registro pubblico delle firme

Questo repository fa da database **append-only** per le petizioni: ad ogni firma
la serverless function aggiorna il file della proposta con un commit pubblico.
Chi ha firmato può verificare che il proprio voto è stato registrato.

## Come verificare il tuo voto

1. Recupera il tuo **codice personale** dalla pagina della proposta
   (azione "Verifica", serve rifare il login Google).
2. Apri il file `proposta_<ID>.json` della proposta.
3. Cerca il tuo codice: deve comparire come valore del campo `verifier`.

La cronologia dei commit mostra quando ogni firma è entrata.

## Formato di una riga

```json
{
  "verifier": "3f2a91c47e0b8d65a1f0c93e7b24d8a1",
  "timestamp": "2026-09-14T09:21:44.108Z",
  "dominio": "scuola.it"
}
```

## Privacy

Nessuna email, nessun nome, nessun JWT. Il `verifier` è derivato dall'email con
scrypt e un segreto (`VERIFIER_PEPPER`) che resta sul server: senza quel segreto
non è invertibile né enumerabile. Il dominio email è l'unica parte visibile.
