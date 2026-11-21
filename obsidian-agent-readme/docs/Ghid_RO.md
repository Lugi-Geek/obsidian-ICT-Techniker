# Obsidian-Agent – Ghid de utilizare

Obsidian-Agent este o interfață web locală pentru **managementul proiectelor în Obsidian**. Proiectele, sarcinile, procesele-verbale, deciziile, riscurile, ședințele periodice și echipa sunt salvate ca fișiere Markdown obișnuite în vault-ul Obsidian. O mică bază de date servește doar ca index și planificator zilnic și poate fi reconstruită oricând din vault.

- Rulează numai pe computerul dumneavoastră: `http://127.0.0.1:5055`. Nu se trimit date pe internet.
- Puteți lucra oricând direct în Obsidian. Agentul citește totul din nou la următoarea sincronizare.
- Interfață, șabloane și nume de dosare în germană, engleză, franceză, italiană, spaniolă și română.

## 1. Instalare

### Windows

1. Faceți dublu clic pe `Obsidian-Agent-Setup-2.0.0.exe`. Nu sunt necesare drepturi de administrator.
2. Dacă apare „Windows a protejat PC-ul”, faceți clic pe **Mai multe informații → Rulează oricum**. Programul de instalare nu este semnat cu un certificat plătit.
3. Alegeți limba și urmați pașii de instalare.
4. Apoi instalarea configurează automat:
   - **Python**, dacă lipsește (prin winget, altfel direct de pe python.org),
   - **vault-ul** dumneavoastră (fereastră de selectare, posibil în spatele ferestrei),
   - **pornirea automată** în fundal la fiecare autentificare și **sincronizarea zilnică**,
   - scurtături în **meniul Start** și pe **desktop**.
5. Browserul se deschide cu agentul.

Dosarul programului: `%LOCALAPPDATA%\Programs\Obsidian-Agent` · Setări și bază de date: `%LOCALAPPDATA%\Obsidian-Agent`

### macOS

1. Faceți dublu clic pe `Obsidian-Agent-2.0.0.pkg`.
2. Dacă macOS anunță că pachetul nu poate fi verificat, alegeți **Configurări sistem → Confidențialitate și securitate → Deschide oricum** (versiuni mai vechi: clic dreapta pe pachet → Deschide). Pachetul nu este semnat cu un certificat de dezvoltator Apple.
3. Urmați pașii de instalare și introduceți parola de administrator.
4. După copiere, pachetul configurează automat: Python (de pe python.org, dacă lipsește), limba Mac-ului, vault-ul (fereastră de selectare), pornirea automată și sincronizarea zilnică.
5. Apoi deschideți agentul din **Aplicații → Obsidian-Agent**.

Dacă vault-ul se află în *Documente*, pe *Desktop* sau în *iCloud Drive*, macOS poate bloca sincronizarea în fundal. Pachetul detectează acest lucru și afișează fișierul pe care trebuie să-l adăugați în **Configurări sistem → Confidențialitate și securitate → Acces complet la disc**.

Program: `/Applications/Obsidian-Agent` · Setări și bază de date: `~/Library/Application Support/Obsidian-Agent` · Jurnal de instalare: `/tmp/obsidian-agent-install.log`

### Fără instalare (toate sistemele)

Este suficient Python 3.9 sau mai nou. Dezarhivați dosarul `obsidian-agent` și porniți `start.bat` (Windows) sau `start.sh` (macOS/Linux). Flask este deja inclus. Setările sunt salvate atunci în dosarul programului. Pentru sincronizarea zilnică pe Linux adăugați `0 4 * * * cd /cale/obsidian-agent && python3 agent.py sync --geplant` cu `crontab -e`.

## 2. Primii pași

1. **Setări**: verificați calea vault-ului și alegeți limba.
2. **Echipă**: înregistrați membrii cu nume și inițiale.
3. **Proiecte**: creați primul proiect. Se creează structura de dosare de mai jos.
4. Creați **sarcini** și documente de proiect în **Documente**.
5. Pentru ședințele regulate, creați o serie de **Ședințe periodice**.

## 3. Zonele interfeței

| Zonă | Scop |
|---|---|
| **Azi** | Sarcinile de azi și cele întârziate, termene apropiate, notițe modificate recent, sarcină nouă. |
| **Sarcini** | Toate sarcinile pe grupuri, filtru pe proiect, finalizare cu un clic, schimbarea stării, mutare cu „+1 zi”. |
| **Proiecte** | Crearea proiectelor cu structură fixă, completarea proiectelor incomplete. |
| **Documente** | Documente de proiect din șabloane, salvate automat în dosarul potrivit al proiectului. |
| **Din șablon** | Notiță nouă din orice șablon din dosarul de șabloane, inclusiv cele proprii. |
| **Ședințe periodice** | Serii de ședințe cu frecvență, notițe de ședință și acțiuni. Fiecare ședință nouă conține acțiunile deschise. |
| **Echipă** | Fișe cu rol, contact, înlocuitor și sarcinile deschise ale fiecărei persoane. |
| **Căutare** | Căutare în text complet în tot vault-ul. |
| **Setări** | Limba, calea vault-ului, numele dosarelor, ora de sincronizare, jurnalul. |

Fiecare titlu este un link `obsidian://` care deschide notița direct în Obsidian.

## 4. Dosare în vault

| Dosar | Conținut |
|---|---|
| `Proiecte/` | Un subdosar pentru fiecare proiect (structura mai jos) |
| `Sarcini/` | Sarcini fără proiect |
| `Notite/` | Documente fără proiect |
| `_Sabloane/` | Șabloane, editabile în Obsidian |
| `Planificator/` | Rezumatul zilei și arhiva (automat) |
| `Echipa/` | O notiță pentru fiecare membru |
| `Sedinte/` | Un subdosar pentru fiecare serie, cu ședințe și acțiuni |

## 5. Structura proiectului

Fiecare proiect primește o notiță de prezentare `_Proiect_<Nume>.md` (obiective, jaloane, sarcini deschise) și aceste subdosare, fiecare cu un fișier `readme`:

| Dosar | Conținut |
|---|---|
| `01_Mandat_si_Contracte/` | Mandatul proiectului, oferte, contracte, comenzi și acte adiționale. |
| `02_Parti_interesate/` | Sponsor, persoane de contact, roluri, escaladare și comunicare. |
| `03_Planificare/` | Planul proiectului, jaloane, resurse, buget și decizii. |
| `04_Implementare/` | Livrabile, concepte, documentație tehnică și teste. |
| `05_Riscuri_si_Modificari/` | Riscuri, puncte deschise și cereri de modificare. |
| `06_Raportare/` | Rapoarte de stare, indicatori și comitet de coordonare. |
| `07_Procese-verbale/` | Procese-verbale, ședințe periodice și corespondență importantă. |
| `08_Inchidere/` | Recepție, predare către operare și lecții învățate. |

„Completează toate proiectele” adaugă dosarele lipsă la proiectele existente. Nu se suprascrie niciodată nimic.

## 6. Documente de proiect

| Document | Dosar | Nume fișier |
|---|---|---|
| **Proces-verbal** | `07_Procese-verbale/` | `YYYY-MM-DD_PV_….md` |
| **Decizie** | `03_Planificare/` | `Decizie_YYYY-MM-DD_….md` |
| **Risc** | `05_Riscuri_si_Modificari/` | `Risc_….md` |
| **Cerere de modificare** | `05_Riscuri_si_Modificari/` | `Modificare_YYYY-MM-DD_….md` |
| **Parte interesată / contact** | `02_Parti_interesate/` | `Parte_interesata_….md` |
| **Raport de stare** | `06_Raportare/` | `Raport_YYYY-MM_….md` |
| **Închiderea proiectului** | `08_Inchidere/` | `Inchidere_….md` |

Creați și câte o sarcină pentru fiecare acțiune dintr-un proces-verbal, ca să apară la Azi și în echipă.

## 7. Formatul sarcinilor

```markdown
---
typ: task
titel: Pregătirea kick-off-ului
projekt: Migrare M365
start: 2026-11-18
ende: 2026-11-20
status: offen            # offen | in_arbeit | wartend | erledigt
prioritaet: hoch         # hoch | mittel | niedrig
verantwortlich: AM       # numele sau inițialele unui membru al echipei
---
- [ ] Pasul 1
- [x] Pasul 2
```

- **Azi**: început ≤ azi ≤ sfârșit · **Întârziată**: sfârșit < azi · **Planificată**: început > azi.
- Dacă lipsește `status`, o sarcină este considerată finalizată când toate căsuțele sunt bifate.
- Numele câmpurilor din frontmatter (`typ`, `titel`, `ende` = sfârșit, `verantwortlich` = responsabil …) sunt aceleași în toate limbile. Astfel agentul poate citi orice vault, chiar și după schimbarea limbii.

## 8. Rezumatul zilei și sincronizarea

În fiecare zi la ora 04:00 (configurabil), agentul citește toate notițele și scrie rezumatul zilei în `Planificator/Azi.md`, plus o arhivă pe zi. Astfel vedeți rezumatul și în Obsidian, și pe telefon. Dacă computerul a fost oprit, rularea este recuperată. „Actualizează acum” citește imediat vault-ul.

## 9. Schimbarea limbii

În stânga jos, în navigare, sau în **Setări**. Interfața se schimbă imediat. Șabloanele noi sunt create în limba aleasă. Într-un vault fără proiecte se adaptează și numele dosarelor și structura proiectului. Dosarele și notițele existente nu sunt niciodată redenumite.

## 10. Adaptarea șabloanelor

Toate șabloanele se află în dosarul de șabloane al vault-ului și pot fi editate în Obsidian. Substituenți: `{{title}}`, `{{date}}`, `{{projekt}}`. Cu `zielordner: 03_…` în frontmatter-ul unui șablon propriu stabiliți dosarul preselectat. Șabloanele standard șterse sunt recreate la următoarea sincronizare.

## 11. Opțional: Dataview

Prezentările de proiect conțin o interogare Dataview a sarcinilor deschise. Pentru aceasta, activați în Obsidian pluginul comunității **Dataview**. Agentul în sine nu are nevoie de el.

## 12. Actualizare, copie de siguranță, dezinstalare

- **Actualizare**: instalați pur și simplu noul program de instalare sau pachet. Setările și baza de date se păstrează.
- **Copie de siguranță**: vault-ul este sursa de adevăr. Baza de date conține în plus doar istoricul zilnic.
- **Dezinstalare pe Windows**: *Setări → Aplicații → Obsidian-Agent → Dezinstalare*.
- **Dezinstalare pe macOS**: *Aplicații → Obsidian-Agent → Dezinstalare Obsidian-Agent*.
- Ambele salvează `config.json` și `planer.db` într-un dosar `obsidian-agent-backup_<dată>` pe desktop. **Vault-ul Obsidian nu este niciodată modificat sau șters.**

## 13. Rezolvarea problemelor

| Problemă | Soluție |
|---|---|
| Browserul afișează „site inaccesibil” | Deschideți agentul din meniul Start / Aplicații. Jurnal: `logs/gui.log` în dosarul de setări. |
| Lipsesc notițe noi în interfață | Faceți clic pe „Actualizează acum”. Verificați numele fișierului `Task_…` sau câmpul `typ:`. |
| O sarcină nu apare la un membru al echipei | Folosiți în câmpul `verantwortlich` numele complet sau inițialele din echipă. |
| macOS: sincronizarea în fundal eșuează | Permiteți accesul complet la disc pentru fișierul Python afișat (vezi instalarea). |
| Portul 5055 este ocupat | Modificați `port` în `config.json` și reporniți agentul. |

Linie de comandă: `python agent.py sync` · `python agent.py heute` (azi) · `python agent.py projekt "Nume"` · `python agent.py info`

---
[Deutsch](Anleitung_DE.md) · [English](Guide_EN.md) · [Français](Guide_FR.md) · [Italiano](Guida_IT.md) · [Español](Guia_ES.md)
