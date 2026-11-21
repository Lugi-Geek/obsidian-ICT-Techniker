# Obsidian-Agent – Anleitung

Obsidian-Agent ist eine lokale Weboberfläche für das **Projektmanagement in Obsidian**. Projekte, Tasks, Protokolle, Entscheidungen, Risiken, Jour Fixes und das Team werden als normale Markdown-Dateien in Ihrem Obsidian-Vault abgelegt. Eine kleine Datenbank dient nur als Index und Tagesplaner und wird jederzeit aus dem Vault neu aufgebaut.

- Läuft nur auf Ihrem Computer: `http://127.0.0.1:5055`. Es werden keine Daten ins Internet übertragen.
- Sie können jederzeit direkt in Obsidian arbeiten. Der Agent liest beim nächsten Sync alles wieder ein.
- Oberfläche, Vorlagen und Ordnernamen in Deutsch, Englisch, Französisch, Italienisch, Spanisch und Rumänisch.

## 1. Installation

### Windows

1. `Obsidian-Agent-Setup-2.0.0.exe` doppelklicken. Administratorrechte sind nicht nötig.
2. Erscheint «Der Computer wurde durch Windows geschützt», auf **Weitere Informationen → Trotzdem ausführen** klicken. Das Setup ist nicht mit einem kostenpflichtigen Zertifikat signiert.
3. Sprache wählen und der Installation folgen.
4. Das Setup richtet danach automatisch ein:
   - **Python**, falls es fehlt (über winget, sonst direkt von python.org),
   - Ihren **Vault** (Ordner-Dialog, eventuell hinter dem Fenster),
   - den **Autostart** bei jeder Anmeldung im Hintergrund und den **täglichen Sync**,
   - Verknüpfungen im **Startmenü** und auf dem **Desktop**.
5. Der Browser öffnet sich mit dem Agent.

Programmordner: `%LOCALAPPDATA%\Programs\Obsidian-Agent` · Einstellungen und Datenbank: `%LOCALAPPDATA%\Obsidian-Agent`

### macOS

1. `Obsidian-Agent-2.0.0.pkg` doppelklicken.
2. Meldet macOS, dass das Paket nicht geprüft werden kann: **Systemeinstellungen → Datenschutz & Sicherheit → Dennoch öffnen** wählen (bei älteren Versionen: Rechtsklick auf das Paket → Öffnen). Das Paket ist nicht mit einem Apple-Entwicklerzertifikat signiert.
3. Der Installation folgen und das Administratorpasswort eingeben.
4. Nach dem Kopieren richtet das Paket automatisch ein: Python (falls es fehlt, von python.org), die Sprache Ihres Macs, Ihren Vault (Ordner-Dialog), den Autostart und den täglichen Sync.
5. Danach öffnen Sie den Agent über **Programme → Obsidian-Agent**.

Liegt der Vault in *Dokumente*, auf dem *Schreibtisch* oder in *iCloud Drive*, kann macOS den Hintergrund-Sync blockieren. Das Paket erkennt das und zeigt die Datei an, die Sie unter **Systemeinstellungen → Datenschutz & Sicherheit → Festplattenvollzugriff** hinzufügen müssen.

Programm: `/Applications/Obsidian-Agent` · Einstellungen und Datenbank: `~/Library/Application Support/Obsidian-Agent` · Installationsprotokoll: `/tmp/obsidian-agent-install.log`

### Ohne Installation (alle Systeme)

Python 3.9 oder neuer genügt. Ordner `obsidian-agent` entpacken und `start.bat` (Windows) bzw. `start.sh` (macOS/Linux) starten. Flask ist bereits enthalten. Einstellungen liegen dann im Programmordner. Für den täglichen Sync unter Linux: `0 4 * * * cd /pfad/obsidian-agent && python3 agent.py sync --geplant` in `crontab -e`.

## 2. Erste Schritte

1. **Einstellungen**: Vault-Pfad prüfen, Sprache wählen.
2. **Team**: Teammitglieder mit Name und Kürzel erfassen.
3. **Projekte**: erstes Projekt anlegen. Es entsteht die Ordnerstruktur unten.
4. **Tasks** anlegen, Projektdokumente unter **Dokumentation** erstellen.
5. Für wiederkehrende Sitzungen eine **Jour Fixe**-Serie anlegen.

## 3. Bereiche der Oberfläche

| Bereich | Zweck |
|---|---|
| **Heute** | Heutige und überfällige Tasks, demnächst Fälliges, zuletzt geänderte Notizen, neuen Task anlegen. |
| **Tasks** | Alle Tasks nach Gruppen, Filter nach Projekt, mit einem Klick erledigt, Status ändern, «+1 Tag» verschieben. |
| **Projekte** | Projekte mit fester Struktur anlegen, unvollständige Projekte ergänzen. |
| **Dokumentation** | Projektdokumente aus Vorlagen. Sie landen automatisch im passenden Projektordner. |
| **Aus Vorlage** | Neue Notiz aus jeder Vorlage im Vorlagen-Ordner, auch aus eigenen Vorlagen. |
| **Jour Fixe** | Sitzungsserien mit Turnus, Sitzungsnotizen und Pendenzen. Jede neue Sitzung enthält die offenen Pendenzen. |
| **Team** | Personenkarten mit Rolle, Kontakt, Vertretung und den offenen Tasks jeder Person. |
| **Suche** | Volltextsuche über den ganzen Vault. |
| **Einstellungen** | Sprache, Vault-Pfad, Ordnernamen, Sync-Zeit, Sync-Protokoll. |

Jeder Titel ist ein `obsidian://`-Link und öffnet die Notiz direkt in Obsidian.

## 4. Ordner im Vault

| Ordner | Inhalt |
|---|---|
| `Projekte/` | Ein Unterordner pro Projekt (Struktur siehe unten) |
| `Tasks/` | Tasks ohne Projekt |
| `Notizen/` | Dokumente ohne Projekt |
| `_Vorlagen/` | Vorlagen, in Obsidian anpassbar |
| `Planer/` | Tagesübersicht und Archiv (automatisch) |
| `Team/` | Eine Notiz pro Teammitglied |
| `JourFixe/` | Ein Unterordner pro Serie mit Sitzungen und Pendenzen |

## 5. Projektstruktur

Jedes Projekt erhält eine Übersichtsnotiz `_Projekt_<Name>.md` (Ziele, Meilensteine, offene Tasks) und diese Unterordner, jeweils mit einer `readme`-Datei:

| Ordner | Inhalt |
|---|---|
| `01_Auftrag_und_Vertraege/` | Projektauftrag, Angebote, Verträge, Bestellungen und Nachträge. |
| `02_Stakeholder/` | Auftraggeber, Ansprechpartner, Rollen, Eskalation und Kommunikation. |
| `03_Planung/` | Projektplan, Meilensteine, Ressourcen, Budget und Entscheidungen. |
| `04_Umsetzung/` | Arbeitsergebnisse, Konzepte, technische Dokumentation und Tests. |
| `05_Risiken_und_Changes/` | Risiken, offene Punkte und Änderungsanträge (Changes). |
| `06_Reporting/` | Statusberichte, Kennzahlen und Lenkungsausschuss. |
| `07_Protokolle/` | Sitzungsprotokolle, Jour Fixe und wichtige Korrespondenz. |
| `08_Abschluss/` | Abnahme, Übergabe in den Betrieb und Lessons Learned. |

Mit «Alle Projekte ergänzen» erhalten bestehende Projekte fehlende Ordner. Es wird nie etwas überschrieben.

## 6. Projektdokumente

| Dokument | Ordner | Dateiname |
|---|---|---|
| **Sitzungsprotokoll** | `07_Protokolle/` | `JJJJ-MM-TT_Protokoll_….md` |
| **Entscheidung** | `03_Planung/` | `Entscheidung_JJJJ-MM-TT_….md` |
| **Risiko** | `05_Risiken_und_Changes/` | `Risiko_….md` |
| **Änderungsantrag (Change)** | `05_Risiken_und_Changes/` | `Change_JJJJ-MM-TT_….md` |
| **Stakeholder / Kontakt** | `02_Stakeholder/` | `Stakeholder_….md` |
| **Statusbericht** | `06_Reporting/` | `Statusbericht_JJJJ-MM_….md` |
| **Projektabschluss** | `08_Abschluss/` | `Projektabschluss_….md` |

Aktionspunkte aus Protokollen zusätzlich als Task anlegen, damit sie unter Heute und im Team erscheinen.

## 7. Task-Format

```markdown
---
typ: task
titel: Kick-off vorbereiten
projekt: Migration M365
start: 2026-11-18
ende: 2026-11-20
status: offen            # offen | in_arbeit | wartend | erledigt
prioritaet: hoch         # hoch | mittel | niedrig
verantwortlich: AM       # Name oder Kürzel aus dem Team
---
- [ ] Schritt 1
- [x] Schritt 2
```

- **Heute**: Start ≤ heute ≤ Ende · **Überfällig**: Ende < heute · **Geplant**: Start > heute.
- Fehlt `status`, gilt ein Task als erledigt, wenn alle Checkboxen abgehakt sind.
- Die Feldnamen im Frontmatter sind in allen Sprachen gleich. So kann der Agent jeden Vault lesen, auch nach einem Sprachwechsel.

## 8. Tägliche Übersicht und Sync

Täglich um 04:00 (einstellbar) liest der Agent alle Notizen ein und schreibt die Tagesübersicht nach `Planer/Heute.md`, zusätzlich ein Archiv pro Tag. So sehen Sie die Übersicht auch in Obsidian und auf dem Handy. War der Computer aus, wird der Lauf nachgeholt. «Jetzt aktualisieren» liest den Vault sofort ein.

## 9. Sprache wechseln

Unten links in der Navigation oder unter **Einstellungen**. Die Oberfläche wechselt sofort. Neue Vorlagen werden in der gewählten Sprache angelegt. In einem Vault ohne Projekte werden auch Ordnernamen und Projektstruktur angepasst. Bestehende Ordner und Notizen werden nie umbenannt.

## 10. Vorlagen anpassen

Alle Vorlagen liegen im Vorlagen-Ordner des Vaults und können in Obsidian bearbeitet werden. Platzhalter: `{{title}}`, `{{date}}`, `{{projekt}}`. Mit `zielordner: 03_…` im Frontmatter einer eigenen Vorlage bestimmen Sie den vorgewählten Ordner. Gelöschte Standardvorlagen werden beim nächsten Sync neu angelegt.

## 11. Optional: Dataview

Die Projektübersichten enthalten eine Dataview-Abfrage der offenen Tasks. Dafür das Community-Plugin **Dataview** in Obsidian aktivieren. Für den Agent selbst ist es nicht nötig.

## 12. Update, Sicherung, Deinstallation

- **Update**: neues Setup bzw. Paket einfach installieren. Einstellungen und Datenbank bleiben erhalten.
- **Sicherung**: Der Vault ist die Wahrheit. Die Datenbank enthält nur zusätzlich die Tageshistorie.
- **Deinstallation Windows**: *Einstellungen → Apps → Obsidian-Agent → Deinstallieren*.
- **Deinstallation macOS**: *Programme → Obsidian-Agent → Obsidian-Agent deinstallieren*.
- Beide sichern `config.json` und `planer.db` in einen Ordner `obsidian-agent-backup_<Datum>` auf dem Desktop. **Der Obsidian-Vault wird nie verändert oder gelöscht.**

## 13. Hilfe bei Problemen

| Problem | Lösung |
|---|---|
| Browser zeigt «Seite nicht erreichbar» | Agent über Startmenü / Programme öffnen. Protokoll: `logs/gui.log` im Einstellungsordner. |
| Neue Notizen fehlen in der Oberfläche | «Jetzt aktualisieren» klicken. Dateiname `Task_…` bzw. Feld `typ:` prüfen. |
| Task erscheint nicht beim Teammitglied | Im Feld `verantwortlich` den vollen Namen oder das Kürzel aus dem Team verwenden. |
| macOS: Sync im Hintergrund schlägt fehl | Festplattenvollzugriff für die angezeigte Python-Datei erlauben (siehe Installation). |
| Port 5055 belegt | In `config.json` den Wert `port` ändern und den Agent neu starten. |

Kommandozeile: `python agent.py sync` · `python agent.py heute` · `python agent.py projekt "Name"` · `python agent.py info`

---
[English](Guide_EN.md) · [Français](Guide_FR.md) · [Italiano](Guida_IT.md) · [Español](Guia_ES.md) · [Română](Ghid_RO.md)
