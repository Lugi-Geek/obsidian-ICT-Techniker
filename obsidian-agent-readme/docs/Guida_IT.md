# Obsidian-Agent – Guida

Obsidian-Agent è un'interfaccia web locale per la **gestione dei progetti in Obsidian**. Progetti, attività, verbali, decisioni, rischi, riunioni periodiche e team vengono salvati come normali file Markdown nel vostro vault di Obsidian. Un piccolo database serve solo da indice e agenda giornaliera e viene ricostruito dal vault in qualsiasi momento.

- Funziona solo sul vostro computer: `http://127.0.0.1:5055`. Nessun dato viene inviato in Internet.
- Potete sempre lavorare direttamente in Obsidian. L'agente rilegge tutto alla sincronizzazione successiva.
- Interfaccia, modelli e nomi delle cartelle in tedesco, inglese, francese, italiano, spagnolo e rumeno.

## 1. Installazione

### Windows

1. Fare doppio clic su `Obsidian-Agent-Setup-2.0.0.exe`. Non servono diritti di amministratore.
2. Se compare «Windows ha protetto il PC», fare clic su **Ulteriori informazioni → Esegui comunque**. Il programma di installazione non è firmato con un certificato a pagamento.
3. Scegliere la lingua e seguire l'installazione.
4. L'installazione configura poi automaticamente:
   - **Python**, se manca (tramite winget, altrimenti direttamente da python.org),
   - il vostro **vault** (finestra di selezione, eventualmente dietro la finestra),
   - l'**avvio automatico** in background a ogni accesso e la **sincronizzazione giornaliera**,
   - collegamenti nel **menu Start** e sul **desktop**.
5. Il browser si apre con l'agente.

Cartella del programma: `%LOCALAPPDATA%\Programs\Obsidian-Agent` · Impostazioni e database: `%LOCALAPPDATA%\Obsidian-Agent`

### macOS

1. Fare doppio clic su `Obsidian-Agent-2.0.0.pkg`.
2. Se macOS segnala che il pacchetto non può essere verificato, scegliere **Impostazioni di Sistema → Privacy e sicurezza → Apri comunque** (versioni precedenti: clic destro sul pacchetto → Apri). Il pacchetto non è firmato con un certificato sviluppatore Apple.
3. Seguire l'installazione e inserire la password di amministratore.
4. Dopo la copia il pacchetto configura automaticamente: Python (da python.org, se manca), la lingua del Mac, il vault (finestra di selezione), l'avvio automatico e la sincronizzazione giornaliera.
5. In seguito aprire l'agente da **Applicazioni → Obsidian-Agent**.

Se il vault si trova in *Documenti*, sulla *Scrivania* o in *iCloud Drive*, macOS può bloccare la sincronizzazione in background. Il pacchetto lo rileva e mostra il file da aggiungere in **Impostazioni di Sistema → Privacy e sicurezza → Accesso completo al disco**.

Programma: `/Applications/Obsidian-Agent` · Impostazioni e database: `~/Library/Application Support/Obsidian-Agent` · Registro di installazione: `/tmp/obsidian-agent-install.log`

### Senza installazione (tutti i sistemi)

Basta Python 3.9 o successivo. Estrarre la cartella `obsidian-agent` e avviare `start.bat` (Windows) o `start.sh` (macOS/Linux). Flask è già incluso. Le impostazioni vengono salvate nella cartella del programma. Per la sincronizzazione giornaliera su Linux aggiungere `0 4 * * * cd /percorso/obsidian-agent && python3 agent.py sync --geplant` con `crontab -e`.

## 2. Primi passi

1. **Impostazioni**: verificare il percorso del vault, scegliere la lingua.
2. **Team**: registrare i membri con nome e sigla.
3. **Progetti**: creare il primo progetto. Viene creata la struttura di cartelle qui sotto.
4. Creare **attività** e documenti di progetto in **Documenti**.
5. Per le riunioni regolari creare una serie di **Riunioni periodiche**.

## 3. Aree dell'interfaccia

| Area | Scopo |
|---|---|
| **Oggi** | Attività di oggi e scadute, prossime scadenze, note modificate di recente, nuova attività. |
| **Attività** | Tutte le attività per gruppo, filtro per progetto, completare con un clic, cambiare stato, spostare di «+1 giorno». |
| **Progetti** | Creare progetti con struttura fissa, completare progetti incompleti. |
| **Documenti** | Documenti di progetto da modelli, salvati automaticamente nella cartella giusta del progetto. |
| **Da modello** | Nuova nota da qualsiasi modello della cartella dei modelli, anche dai vostri. |
| **Riunioni periodiche** | Serie di riunioni con frequenza, note di riunione e azioni. Ogni nuova riunione contiene le azioni aperte. |
| **Team** | Schede con ruolo, contatto, sostituto e le attività aperte di ogni persona. |
| **Ricerca** | Ricerca a testo pieno in tutto il vault. |
| **Impostazioni** | Lingua, percorso del vault, nomi delle cartelle, ora di sincronizzazione, registro. |

Ogni titolo è un link `obsidian://` che apre la nota direttamente in Obsidian.

## 4. Cartelle nel vault

| Cartella | Contenuto |
|---|---|
| `Progetti/` | Una sottocartella per progetto (struttura qui sotto) |
| `Attivita/` | Attività senza progetto |
| `Note/` | Documenti senza progetto |
| `_Modelli/` | Modelli, modificabili in Obsidian |
| `Agenda/` | Riepilogo del giorno e archivio (automatico) |
| `Team/` | Una nota per membro del team |
| `Riunioni/` | Una sottocartella per serie con riunioni e azioni |

## 5. Struttura del progetto

Ogni progetto riceve una nota di panoramica `_Progetto_<Nome>.md` (obiettivi, milestone, attività aperte) e queste sottocartelle, ciascuna con un file `readme`:

| Cartella | Contenuto |
|---|---|
| `01_Mandato_e_Contratti/` | Mandato di progetto, offerte, contratti, ordini e aggiunte. |
| `02_Stakeholder/` | Committente, referenti, ruoli, escalation e comunicazione. |
| `03_Pianificazione/` | Piano di progetto, milestone, risorse, budget e decisioni. |
| `04_Esecuzione/` | Risultati, concetti, documentazione tecnica e test. |
| `05_Rischi_e_Modifiche/` | Rischi, punti aperti e richieste di modifica. |
| `06_Reporting/` | Rapporti di stato, indicatori e comitato direttivo. |
| `07_Verbali/` | Verbali, riunioni periodiche e corrispondenza importante. |
| `08_Chiusura/` | Collaudo, passaggio all'esercizio e lezioni apprese. |

«Completa tutti i progetti» aggiunge le cartelle mancanti ai progetti esistenti. Non viene mai sovrascritto nulla.

## 6. Documenti di progetto

| Documento | Cartella | Nome file |
|---|---|---|
| **Verbale** | `07_Verbali/` | `YYYY-MM-DD_Verbale_….md` |
| **Decisione** | `03_Pianificazione/` | `Decisione_YYYY-MM-DD_….md` |
| **Rischio** | `05_Rischi_e_Modifiche/` | `Rischio_….md` |
| **Richiesta di modifica** | `05_Rischi_e_Modifiche/` | `Modifica_YYYY-MM-DD_….md` |
| **Stakeholder / contatto** | `02_Stakeholder/` | `Stakeholder_….md` |
| **Rapporto di stato** | `06_Reporting/` | `Rapporto_YYYY-MM_….md` |
| **Chiusura del progetto** | `08_Chiusura/` | `Chiusura_….md` |

Create anche un'attività per ogni azione di un verbale, così compare in Oggi e nel team.

## 7. Formato delle attività

```markdown
---
typ: task
titel: Preparare il kick-off
projekt: Migrazione M365
start: 2026-11-18
ende: 2026-11-20
status: offen            # offen | in_arbeit | wartend | erledigt
prioritaet: hoch         # hoch | mittel | niedrig
verantwortlich: AM       # nome o sigla di un membro del team
---
- [ ] Passo 1
- [x] Passo 2
```

- **Oggi**: inizio ≤ oggi ≤ fine · **Scaduta**: fine < oggi · **Pianificata**: inizio > oggi.
- Senza `status`, un'attività è considerata completata quando tutte le caselle sono spuntate.
- I nomi dei campi del frontmatter (`typ`, `titel`, `ende` = fine, `verantwortlich` = responsabile …) sono uguali in tutte le lingue. Così l'agente legge qualsiasi vault, anche dopo un cambio di lingua.

## 8. Riepilogo del giorno e sincronizzazione

Ogni giorno alle 04:00 (impostabile) l'agente legge tutte le note e scrive il riepilogo del giorno in `Agenda/Oggi.md`, più un archivio giornaliero. Il riepilogo è quindi visibile anche in Obsidian e sul telefono. Se il computer era spento, l'esecuzione viene recuperata. «Aggiorna ora» legge subito il vault.

## 9. Cambiare lingua

In basso a sinistra nella navigazione oppure in **Impostazioni**. L'interfaccia cambia subito. I nuovi modelli vengono creati nella lingua scelta. In un vault senza progetti vengono adattati anche i nomi delle cartelle e la struttura di progetto. Cartelle e note esistenti non vengono mai rinominate.

## 10. Personalizzare i modelli

Tutti i modelli si trovano nella cartella dei modelli del vault e si possono modificare in Obsidian. Segnaposto: `{{title}}`, `{{date}}`, `{{projekt}}`. Con `zielordner: 03_…` nel frontmatter di un modello personalizzato definite la cartella preselezionata. I modelli standard eliminati vengono ricreati alla sincronizzazione successiva.

## 11. Facoltativo: Dataview

Le panoramiche dei progetti contengono una query Dataview delle attività aperte. Per usarla attivare in Obsidian il plugin della community **Dataview**. L'agente stesso non ne ha bisogno.

## 12. Aggiornamento, backup, disinstallazione

- **Aggiornamento**: installare semplicemente il nuovo programma o pacchetto. Impostazioni e database restano invariati.
- **Backup**: il vault è la fonte di verità. Il database contiene in più solo la cronologia giornaliera.
- **Disinstallazione Windows**: *Impostazioni → App → Obsidian-Agent → Disinstalla*.
- **Disinstallazione macOS**: *Applicazioni → Obsidian-Agent → Disinstalla Obsidian-Agent*.
- Entrambe salvano `config.json` e `planer.db` in una cartella `obsidian-agent-backup_<data>` sul desktop. **Il vault di Obsidian non viene mai modificato né eliminato.**

## 13. Risoluzione dei problemi

| Problema | Soluzione |
|---|---|
| Il browser mostra «sito non raggiungibile» | Aprire l'agente dal menu Start / Applicazioni. Registro: `logs/gui.log` nella cartella delle impostazioni. |
| Nuove note mancano nell'interfaccia | Fare clic su «Aggiorna ora». Verificare il nome del file `Task_…` o il campo `typ:`. |
| Un'attività non compare presso un membro | Usare nel campo `verantwortlich` il nome completo o la sigla del team. |
| macOS: la sincronizzazione in background fallisce | Consentire l'accesso completo al disco per il file Python indicato (vedi installazione). |
| La porta 5055 è occupata | Modificare `port` in `config.json` e riavviare l'agente. |

Riga di comando: `python agent.py sync` · `python agent.py heute` (oggi) · `python agent.py projekt "Nome"` · `python agent.py info`

---
[Deutsch](Anleitung_DE.md) · [English](Guide_EN.md) · [Français](Guide_FR.md) · [Español](Guia_ES.md) · [Română](Ghid_RO.md)
