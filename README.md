# ROOTS
### From Proof of Family to Proof of Personhood

> *"Le radici di un albero morto nutrono la terra attorno — non solo i rami che gli erano più vicini."*

**ROOTS** è un esperimento sociale rurale sulla rete Kusama. Prende il più antico sistema anti-Sybil della storia umana — la tradizione orale dei soprannomi familiari in un piccolo villaggio dell'Italia meridionale — e lo codifica on-chain come un grafo d'identità vivente e in crescita.

Sottomesso alla **KSM Art & Social Experiments Initiative** della Kusama Vision Initiative.

---

## Due asset, due funzioni

Ogni famiglia attestata riceve **due asset on-chain** distinti. Non devono essere confusi.

### Asset 1 — Il ROOTS NFT (identità)

L'NFT è lo **strumento di identità e lignaggio**. È la prima cosa mintata per una famiglia, ed è ciò che rende ogni famiglia unica nel grafo.

Ogni ROOTS NFT è un'opera generativa calcolata dalla posizione della famiglia nel grafo del lignaggio. L'opera **evolve nel tempo**: ogni volta che una sotto-famiglia si ramifica, l'NFT genitore acquisisce un nuovo elemento visivo.

Campi chiave nei metadati:

- `roots_parent_nft_id` — da quale famiglia discende (null per i fondatori)
- `lineage_depth` — generazioni dalla radice del grafo
- `branch_count` — sotto-famiglie dirette ramificate
- `total_descendants` — totale delle famiglie nel sottoalbero
- `succession_address` — wallet del successore designato (null finché non impostato)
- `status` — active / dormant / succeeded
- `token_allocation` — calcolato dall'indicizzatore, aggiornato ad ogni cambio del grafo

**La rarità è strutturale.** Un NFT di una famiglia fondatrice con molti discendenti è più raro di uno di una famiglia registrata di recente. Non è assegnata arbitrariamente — emerge dalla reale dimensione e anzianità della famiglia nel villaggio.

### Asset 2 — Il ROOTS Token (governance)

Il ROOTS Token è lo **strumento di governance**. È un token fungibile mintato via Kusama Asset Hub con `transfer: None` a livello di protocollo. Non può essere venduto, inviato o scambiato. Ha **zero valore monetario**.

Il token **non è statico**: l'allocazione cambia al crescere della famiglia, usando una formula a rendimenti decrescenti che garantisce che nessuna famiglia possa dominare da sola.

---

## Il Meccanismo di Redistribuzione Token

### Il problema della formula lineare

Una formula lineare (`10 + branch*5 + desc*2`) portava il fondatore più grande a circa 145 token in un villaggio di 60 famiglie — l'11% del circolante da solo. Con un accordo tra le top 3, si arrivava al 25%: una minoranza potente poteva determinare il risultato.

### La soluzione: radice quadrata

```
token_allocation(family) =
    10                               # base: dignità uguale per tutti
  + sqrt(branch_count)  × 6         # rendimenti decrescenti sui rami diretti
  + sqrt(total_descendants) × 4     # rendimenti decrescenti sui discendenti totali
  + max(0, 4 - lineage_depth)       # bonus età: 4 per fondatori, poi 3,2,1,0
```

**Proprietà garantite dalla matematica della radice quadrata** (non da un cap artificiale):

| Metrica | Formula lineare | Formula √ |
|---------|-----------------|-----------|
| % max famiglia | 10.8% | 5.6% |
| % top 3 famiglie insieme | 25.2% | 15.0% |
| Ratio max/min | 12×  | 5.3× |

Nessuna famiglia può superare il ~6% del circolante totale. Le top 3 insieme non raggiungono il 15%. Per vincere un referendum, anche le famiglie più grandi devono costruire una coalizione reale.

### Esempio concreto — villaggio di 60 famiglie

| Famiglia | branch | desc | depth | Token | % circolante |
|----------|--------|------|-------|-------|--------------|
| Fondatori A (più grande) | 8 | 45 | 0 | 10+20+27+4 = **61** | 5.9% |
| Fondatori B | 6 | 32 | 0 | 10+15+23+4 = **52** | 5.0% |
| Media (2 rami, 6 disc) | 2 | 6 | 1 | 10+8+10+3 = **31** | 3.0% |
| Famiglia nuova | 0 | 0 | 3 | 10+0+0+1 = **11** | 1.1% |

A e B insieme: **~10.9%** — non bastano. Serve ancora il consenso di altri 4–5 famiglie per avvicinarsi al 50%.

### Trigger di redistribuzione

Il balance viene ricalcolato ogni volta che:

1. Una nuova sotto-famiglia linka il proprio NFT a un genitore (tutta la catena di antenati viene aggiornata)
2. Una famiglia entra in stato dormant o viene rimossa
3. Un evento di successione cambia il wallet titolare
4. Uno snapshot di referendum viene preso

---

## Doppio Quorum

La formula a radice quadrata risolve la **concentrazione del peso**. Ma resta un secondo problema: una famiglia grande potrebbe vincere un referendum con bassa partecipazione, trascinandoci solo le famiglie alleate mentre il resto del villaggio resta a casa.

Per questo motivo un referendum è valido solo se soddisfa **entrambi** i quorum:

```
Quorum A (token):     >50% dei token espressi devono essere a favore
Quorum B (famiglie):  >33% delle famiglie registrate devono aver votato
```

Il Quorum B è la soglia di legittimità popolare. Il peso dei token è il *come* si vota. La partecipazione è il *se* il voto conta.

**Effetto pratico**: anche la famiglia con 61 token (5.9%) non può fare nulla senza portare almeno 20 famiglie su 60 alle urne. Un consiglio di famiglia richiede che il consiglio sia presente.

---

## La Morte del Capostipite

**Questa è la domanda che nessuno fa. Dovrebbe essere la prima.**

Ogni capostipite morirà. Il villaggio è anziano. Alcuni moriranno durante l'esperimento. Quando succede:

1. **La chiave privata è persa.** Il wallet è inaccessibile. Nessuno può firmare.
2. **Il ROOTS Token è bloccato.** Non-trasferibile per design — non può spostarsi sull'erede.
3. **Il ROOTS NFT è orfano.** I figli possono referenziare il suo ID come `roots_parent_nft_id`, ma la partecipazione alla governance della famiglia si ferma.

Le famiglie con più token — le più antiche, le più ramificate — sono anche quelle più probabilmente guidate da patriarchi anziani. Senza protocollo, il sistema si svuota esattamente dove conta di più.

### Cosa succede alla morte

I token del capostipite spariscono. Non si ereditano. Quello che resta è l'NFT della famiglia — la memoria del lignaggio, il nodo da cui i figli continuano a ramificarsi nel grafo.

**Il protocollo è semplice:**

1. **I token vengono bruciati.** Il peso politico del patriarca non si trasmette.
2. **Ogni figlio diretto registrato riceve +1 token** in segno di eredità simbolica — un voto per ricordare che vengono da lui.
3. **L'NFT resta in cima al grafo.** I rami figli continuano a referenziarlo come `roots_parent_nft_id`. La famiglia non scompare — perde solo il capostipite.
4. **Il nuovo capostipite** è designato dalla comunità. Riceve token calcolati dal grafo già esistente: se la famiglia è numerosa, ha già voce naturalmente.

**Esempio — Fondatori A muore (73 token, 8 figli diretti):**
- 73 token bruciati
- 8 figli diretti ricevono +1 token ciascuno (eredità simbolica)
- NFT resta, status rimane nel grafo
- Il nuovo capostipite di quella famiglia ha già 62–73 token nel suo grafo, a seconda di quanti parenti sono registrati

**Succession Address — il caso ideale:**

Alla cerimonia, ogni capostipite ha 2 minuti per firmare il nome del suo successore on-chain (`succession_address`). Se lo fa, alla sua morte il passaggio avviene immediatamente e senza limbi. È la prima cosa che viene chiesta alla cerimonia.

Se non è stata designata una succession_address, la comunità ha 30 giorni per co-firmare un successore (3 token-holder di quartieri diversi — i familiari non possono attestare se stessi).

**Alla cerimonia ogni capostipite sente tre cose:**
1. I tuoi token spariscono con te — non si ereditano.
2. Il tuo NFT resta: è la memoria della tua famiglia.
3. Ogni tuo figlio registrato riceve 1 token in tuo ricordo.

---

## Chiarimenti Tecnici

### Timeline: 14 settimane = 3,5 mesi

| Fase | Descrizione | Settimane |
|------|-------------|-----------|
| 1 | Etnografia Orale & Libro dei Nomi | 1–4 |
| 2 | La Cerimonia di Attestazione | 5–6 |
| 3 | Registrazione On-Chain | 7–8 |
| 4 | L'Esperimento Sociale (OpenGov) | 9–12 |
| 5 | Report & Framework di Replica | 13–14 |

### Trigger Milestone 2

M2 si attiva alla fine della Fase 3 (registrazioni complete). "Referendum lanciato" è l'evento di confine tra Fase 3 e Fase 4. Il *risultato* del referendum è un deliverable M3.

### Gating via OpenSquare

```
Platform:    OpenSquare (opensquare.network)
Gate:        ROOTS Token balance ≥ 1
Quorum A:    >50% token espressi a favore
Quorum B:    >33% famiglie registrate hanno votato
Snapshot:    blocco al lancio del referendum (fine Fase 3)
```

---

## Struttura del Progetto

```
roots/
├── README.md            ← Qui
├── index.html           ← Landing page di navigazione
├── roots_cover.html     ← Cover page / albero interattivo
├── presentation.html    ← Deck interattivo (12 slide)
└── roots_proposal.pdf   ← Proposta tecnica completa (EN)
```

---

## Le Cinque Fasi

| # | Fase | Settimane | Netto DOT | Crypto Tax Italy (33%) | Lordo DOT |
|---|------|-----------|-----------|-------------|-----------|
| 1 | Etnografia Orale & Libro dei Nomi | 1–4 | 7.500 | 3.694 | 11.194 |
| 2 | La Cerimonia di Attestazione | 5–6 | 10.000 | 4.925 | 14.925 |
| 3 | Registrazione On-Chain | 7–8 | 7.500 | 3.694 | 11.194 |
| 4 | L'Esperimento Sociale (OpenGov) | 9–12 | 9.200 | 4.531 | 13.731 |
| 5 | Report & Framework di Replica | 13–14 | 4.200 | 2.069 | 6.269 |
| — | Buffer contingency | — | 3.300 | 1.626 | 4.926 |
| **TOTALE** | **14 settimane / 3,5 mesi** | **1–14** | **41.700** | **20.539** | **62.239** |

> Finanziamento richiesto: **62.239 DOT lordi** (netto operativo: 41.700 DOT / Crypto Tax Italy 33%: 20.539 DOT)

---

## Milestone di Pagamento

| Milestone | Deliverable | Fasi | Netto DOT | Crypto Tax Italy | Lordo DOT | Rilascio |
|-----------|-------------|------|-----------|-------|-----------|----------|
| **M1 — START** | Accordo firmato. Identità on-chain verificata. Coordinatore locale ingaggiato. Raccolta Fase 1 avviata. | Fase 1 | 7.500 | 3.694 | 11.194 | Sett. 1 |
| **M2 — 100+ TOKEN** | 100+ ROOTS NFTs + token on-chain. Indicizzatore redistribuzione live. Libro dei Nomi depositato. Cerimonia documentata. Referendum lanciato. | Fasi 2–3 | 17.500 | 8.619 | 26.119 | Fine sett. 8 |
| **M3 — FINAL** | Referendum chiuso. Risultato al Comune. Documentario. Report su Mirror.xyz. Protocollo successione documentato. Handbook replicazione. | Fasi 4–5 + Contingency | 16.700 | 8.226 | 24.926 | Fine sett. 14 |
| | **TOTALE** | | **41.700** | **20.539** | **62.239** | |

---

## Architettura Tecnica

### Layer Off-Chain
- Sessioni di raccolta orale (bar, case, piazze)
- Libro dei Nomi: archivio cartaceo, 100 copie, depositato presso il Comune
- Indicizzatore grafo lignaggio: legge i metadati NFT da IPFS, calcola allocazioni token, chiama Asset Hub
- Log eventi di successione: registro off-chain di tutti i claim e gli esiti
- Documentazione video di tutte le fasi

### Layer On-Chain (Kusama Asset Hub)
- **Kusama Identity Pallet** — `house_name`, `village_quarter`, `attestation_hash`, `lineage_parent`
- **ROOTS NFT** — non-fungibile, generativo, lignaggio su IPFS, evolve con il grafo
- **ROOTS Token** — fungibile, `transfer: None`, allocato dinamicamente con formula √
- **OpenSquare space** — referendum con doppio quorum (token + famiglie)

### Schema Metadati NFT ROOTS (IPFS)

```json
{
  "name": "ROOTS [Nome di Casa] / [Villaggio]",
  "attributes": [
    { "trait_type": "house_name",           "value": "stringa (dialetto)" },
    { "trait_type": "roots_parent_nft_id",  "value": "nft_id | null" },
    { "trait_type": "lineage_depth",        "value": "integer" },
    { "trait_type": "branch_count",         "value": "integer" },
    { "trait_type": "total_descendants",    "value": "integer" },
    { "trait_type": "token_allocation",     "value": "integer (calcolato)" },
    { "trait_type": "succession_address",   "value": "ss58 | null" },
    { "trait_type": "status",               "value": "active | dormant | succeeded" },
    { "trait_type": "attestation_ipfs_cid", "value": "CID" }
  ],
  "properties": { "transferable": false, "monetary_value": false }
}
```

### Formula Allocazione Token (definitiva)

```
token_allocation = 10
                 + sqrt(branch_count) × 6
                 + sqrt(total_descendants) × 4
                 + max(0, 4 - lineage_depth)

Ricalcolata ogni volta che:
  - Una sotto-famiglia linka questo NFT come roots_parent_nft_id
  - Una sotto-famiglia entra in dormancy o viene rimossa
  - Un evento di successione cambia il wallet titolare
  - Si prende uno snapshot per referendum
```

---

## Domande Aperte

- **Quorum B su OpenSquare**: la piattaforma supporta nativamente un quorum per *numero di partecipanti* oltre che per peso token? Da verificare tecnicamente; alternativa: implementare controllo off-chain con l'indicizzatore.
- **Trust model dell'indicizzatore**: il calcolo delle allocazioni e la redistribuzione dei token sono operazioni fidate nel MVP. Una versione di produzione userebbe un oracle on-chain o un pallet Substrate con lettura diretta da IPFS.
- **Identificazione del quartiere d'appartenenza**: il Livello 2 richiede che i 3 testimoni siano di quartieri diversi. Questo deve essere codificato nei metadati di ogni wallet/NFT al momento della registrazione.
- **Proof of life per patriarchi anziani**: il `remark` annuale è tecnicamente semplice ma richiede che i capostipiti più anziani mantengano accesso al proprio wallet. Serve un protocollo di assistenza locale.

---

## Disclaimer Importanti

**I ROOTS token e gli NFT hanno zero valore monetario.** Non possono essere scambiati, venduti o ceduti. Il meccanismo di redistribuzione crea peso di governance, non valore finanziario. Il progetto opera sotto la legislazione italiana. Tutti i proventi in crypto sono soggetti a Crypto Tax Italy (33%) al momento della conversione in EUR.

---

*ROOTS · Kusama Network · KSM Art & Social Experiments Initiative · 2026*
*Costruito nell'Italia del Sud. Radicato in quattro secoli di tradizione orale.*
