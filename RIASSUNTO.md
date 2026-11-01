# Memo – PWA per memo vocali (ipovedenti)

**Versione:** 1.0.3 · **Repository previsto:** forrom58/memo · **URL:** https://forrom58.github.io/memo/

## Scopo
Registrare brevi memo audio fuori casa **senza guardare lo schermo** e riascoltarli a casa.

## Come si usa
- **Intestazione della home** (come Vault): a sinistra microfono + "Memo", a destra la versione, tutti sulla stessa linea di base; colore #7fa8a3.
- **Apertura senza vista:** gesto **W** a schermo spento (Impostazioni > Gesti a schermo disattivato > Altro > Traccia una W → Memo).
- **Registrare:** tocco ovunque sullo schermo (tranne la barra in basso).
  - Inizio: vibrazione breve + voce "Registro", poi parte il microfono.
  - Fine: nuovo tocco → doppia vibrazione + voce "Salvato, N secondi".
  - Errore: 3 vibrazioni brevi + voce.
  - Si ferma e salva da sola dopo 5 minuti.
  - Dopo il salvataggio prova a chiudersi da sola (`window.close()`, dalla v1.0.1): Android può ignorarlo.
  - Durante la registrazione lo schermo resta acceso (Wake Lock).
- **Ascoltare:** pulsante "Ascolta i memo" in basso → elenco (più recenti in alto) con data, ora, durata, Ascolta/Ferma, Elimina (con conferma).

## File (ordine alfabetico)
- icon-192.png, icon-512.png – icona secondo lo standard di ICONE-DELLE-MIE-APP.md: fascia da y=369, "MEMO" in Barlow Black 132 px (base y=491); sfondo #1F4A4A, fascia #9FC7C2, scritta #143434, microfono #D2E6E3 (linee 18 px, appoggiato sulla fascia)
- index.html – tutta l'app (HTML, CSS, JS)
- manifest.json – nome breve "Memo", sfondo scuro #121619 (evita il lampo chiaro)
- RIASSUNTO.md – questo file
- sw.js – service worker (prima la rete, poi la copia salvata offline)

## Dati tecnici
- Audio: MediaRecorder, formato webm/opus.
- Archivio: IndexedDB `memo-db`, tabella `memo` (id, data, secondi, audio). I memo restano **solo sul telefono**: disinstallando l'app o cancellando i dati del sito si perdono.
- Colori interfaccia: sfondo #121619, pannelli #1c2328, testo #a9b4bb, registrazione in rosso scuro #7a2e2e. Elenco memo: sfondo #08090a, riquadri #27323a senza bordo, compatti; "Ascolta" (#8fb3c2) ed "Elimina" (#c27a7a) sono solo scritte cliccabili in grassetto, senza pulsante; memo in ascolto con riquadro #31424d. Niente giallo, niente superfici chiare.

## Aggiornare l'app
1. Cambiare `VERSIONE` in index.html e il testo `v…` in alto a destra.
2. Cambiare `CACHE` in sw.js con lo stesso numero.
3. Caricare i file su GitHub.

## Limiti
- Non usa i tasti fisici e non registra a schermo spento (impossibile per una PWA).
- Il primo avvio chiede il permesso del microfono: va concesso una volta, a casa.
