# Obsidian-Agent – User guide

Obsidian-Agent is a local web interface for **project management in Obsidian**. Projects, tasks, minutes, decisions, risks, recurring meetings and the team are stored as ordinary Markdown files in your Obsidian vault. A small database serves only as an index and daily planner and is rebuilt from the vault at any time.

- Runs only on your computer: `http://127.0.0.1:5055`. No data is sent to the internet.
- You can always work directly in Obsidian. The agent reads everything again at the next sync.
- Interface, templates and folder names in German, English, French, Italian, Spanish and Romanian.

## 1. Installation

### Windows

1. Double-click `Obsidian-Agent-Setup-2.0.0.exe`. No administrator rights are needed.
2. If “Windows protected your PC” appears, click **More info → Run anyway**. The setup is not signed with a paid certificate.
3. Choose the language and follow the installer.
4. The setup then configures automatically:
   - **Python**, if it is missing (via winget, otherwise directly from python.org),
   - your **vault** (folder dialog, possibly behind the window),
   - **autostart** in the background at every sign-in and the **daily sync**,
   - shortcuts in the **Start menu** and on the **desktop**.
5. Your browser opens with the agent.

Program folder: `%LOCALAPPDATA%\Programs\Obsidian-Agent` · Settings and database: `%LOCALAPPDATA%\Obsidian-Agent`

### macOS

1. Double-click `Obsidian-Agent-2.0.0.pkg`.
2. If macOS reports that the package cannot be verified, choose **System Settings → Privacy & Security → Open Anyway** (on older versions: right-click the package → Open). The package is not signed with an Apple developer certificate.
3. Follow the installer and enter the administrator password.
4. After copying, the package configures automatically: Python (from python.org, if missing), your Mac's language, your vault (folder dialog), autostart and the daily sync.
5. Afterwards, open the agent via **Applications → Obsidian-Agent**.

If the vault is in *Documents*, on the *Desktop* or in *iCloud Drive*, macOS may block the background sync. The package detects this and shows the file you need to add under **System Settings → Privacy & Security → Full Disk Access**.

Program: `/Applications/Obsidian-Agent` · Settings and database: `~/Library/Application Support/Obsidian-Agent` · Installation log: `/tmp/obsidian-agent-install.log`

### Without installation (all systems)

Python 3.9 or later is enough. Unpack the `obsidian-agent` folder and run `start.bat` (Windows) or `start.sh` (macOS/Linux). Flask is already included. Settings are then stored in the program folder. For the daily sync on Linux add `0 4 * * * cd /path/obsidian-agent && python3 agent.py sync --geplant` with `crontab -e`.

## 2. Getting started

1. **Settings**: check the vault path, choose the language.
2. **Team**: add team members with name and initials.
3. **Projects**: create your first project. The folder structure below is created.
4. Create **tasks** and project documents under **Documents**.
5. For regular meetings, create a **Recurring meetings** series.

## 3. Areas of the interface

| Area | Purpose |
|---|---|
| **Today** | Today's and overdue tasks, upcoming items, recently modified notes, create a new task. |
| **Tasks** | All tasks by group, filter by project, mark done with one click, change status, move by “+1 day”. |
| **Projects** | Create projects with a fixed structure, complete incomplete projects. |
| **Documents** | Project documents from templates. They are placed in the matching project folder automatically. |
| **From template** | New note from any template in the templates folder, including your own. |
| **Recurring meetings** | Meeting series with frequency, meeting notes and action items. Each new meeting lists the open action items. |
| **Team** | Person cards with role, contact, deputy and each person's open tasks. |
| **Search** | Full-text search across the whole vault. |
| **Settings** | Language, vault path, folder names, sync time, sync log. |

Every title is an `obsidian://` link and opens the note directly in Obsidian.

## 4. Folders in the vault

| Folder | Contents |
|---|---|
| `Projects/` | One subfolder per project (structure below) |
| `Tasks/` | Tasks without a project |
| `Notes/` | Documents without a project |
| `_Templates/` | Templates, editable in Obsidian |
| `Planner/` | Daily overview and archive (automatic) |
| `Team/` | One note per team member |
| `Recurring_Meetings/` | One subfolder per series with meetings and action items |

## 5. Project structure

Each project gets an overview note `_Project_<Name>.md` (goals, milestones, open tasks) and these subfolders, each with a `readme` file:

| Folder | Contents |
|---|---|
| `01_Mandate_and_Contracts/` | Project mandate, quotes, contracts, purchase orders and amendments. |
| `02_Stakeholders/` | Sponsor, contacts, roles, escalation and communication. |
| `03_Planning/` | Project plan, milestones, resources, budget and decisions. |
| `04_Execution/` | Deliverables, concepts, technical documentation and tests. |
| `05_Risks_and_Changes/` | Risks, open issues and change requests. |
| `06_Reporting/` | Status reports, key figures and steering committee. |
| `07_Minutes/` | Meeting minutes, recurring meetings and important correspondence. |
| `08_Closure/` | Acceptance, handover to operations and lessons learned. |

“Complete all projects” adds missing folders to existing projects. Nothing is ever overwritten.

## 6. Project documents

| Document | Folder | File name |
|---|---|---|
| **Meeting minutes** | `07_Minutes/` | `YYYY-MM-DD_Minutes_….md` |
| **Decision** | `03_Planning/` | `Decision_YYYY-MM-DD_….md` |
| **Risk** | `05_Risks_and_Changes/` | `Risk_….md` |
| **Change request** | `05_Risks_and_Changes/` | `Change_YYYY-MM-DD_….md` |
| **Stakeholder / contact** | `02_Stakeholders/` | `Stakeholder_….md` |
| **Status report** | `06_Reporting/` | `Status_Report_YYYY-MM_….md` |
| **Project closure** | `08_Closure/` | `Project_Closure_….md` |

Also create action items from minutes as tasks so they appear under Today and in the team view.

## 7. Task format

```markdown
---
typ: task
titel: Prepare kick-off
projekt: M365 migration
start: 2026-11-18
ende: 2026-11-20
status: offen            # offen | in_arbeit | wartend | erledigt
prioritaet: hoch         # hoch | mittel | niedrig
verantwortlich: AM       # name or initials from the team
---
- [ ] Step 1
- [x] Step 2
```

- **Today**: start ≤ today ≤ end · **Overdue**: end < today · **Planned**: start > today.
- If `status` is missing, a task counts as done when all checkboxes are ticked.
- The frontmatter field names (`typ`, `titel`, `ende` = end, `verantwortlich` = owner …) are the same in all languages. This lets the agent read every vault, even after a language change.

## 8. Daily overview and sync

Every day at 04:00 (configurable) the agent reads all notes and writes the daily overview to `Planner/Today.md`, plus an archive per day. You can therefore also see the overview in Obsidian and on your phone. If the computer was off, the run is caught up. “Refresh now” reads the vault immediately.

## 9. Changing the language

Bottom left in the navigation or under **Settings**. The interface switches immediately. New templates are created in the chosen language. In a vault without projects, folder names and the project structure are switched as well. Existing folders and notes are never renamed.

## 10. Customising templates

All templates are in the vault's templates folder and can be edited in Obsidian. Placeholders: `{{title}}`, `{{date}}`, `{{projekt}}`. Set `zielordner: 03_…` in the frontmatter of a custom template to preselect its folder. Deleted standard templates are recreated at the next sync.

## 11. Optional: Dataview

The project overviews contain a Dataview query of the open tasks. Enable the **Dataview** community plugin in Obsidian for it. The agent itself does not need it.

## 12. Update, backup, uninstall

- **Update**: simply install the new setup or package. Settings and database are kept.
- **Backup**: the vault is the source of truth. The database only adds the daily history.
- **Uninstall on Windows**: *Settings → Apps → Obsidian-Agent → Uninstall*.
- **Uninstall on macOS**: *Applications → Obsidian-Agent → Uninstall Obsidian-Agent*.
- Both back up `config.json` and `planer.db` to a folder `obsidian-agent-backup_<date>` on the desktop. **Your Obsidian vault is never changed or deleted.**

## 13. Troubleshooting

| Problem | Solution |
|---|---|
| Browser shows “site can't be reached” | Open the agent via the Start menu / Applications. Log: `logs/gui.log` in the settings folder. |
| New notes are missing in the interface | Click “Refresh now”. Check the file name `Task_…` or the field `typ:`. |
| Task does not appear for a team member | Use the full name or the initials from the team in the field `verantwortlich`. |
| macOS: background sync fails | Allow Full Disk Access for the Python file shown (see installation). |
| Port 5055 is in use | Change `port` in `config.json` and restart the agent. |

Command line: `python agent.py sync` · `python agent.py heute` (today) · `python agent.py projekt "Name"` · `python agent.py info`

---
[Deutsch](Anleitung_DE.md) · [Français](Guide_FR.md) · [Italiano](Guida_IT.md) · [Español](Guia_ES.md) · [Română](Ghid_RO.md)
