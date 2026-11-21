# Obsidian-Agent – Guide d'utilisation

Obsidian-Agent est une interface web locale pour la **gestion de projet dans Obsidian**. Projets, tâches, procès-verbaux, décisions, risques, réunions périodiques et équipe sont enregistrés sous forme de fichiers Markdown ordinaires dans votre coffre Obsidian. Une petite base de données sert uniquement d'index et de planning du jour ; elle est reconstruite à tout moment à partir du coffre.

- Fonctionne uniquement sur votre ordinateur : `http://127.0.0.1:5055`. Aucune donnée n'est envoyée sur Internet.
- Vous pouvez toujours travailler directement dans Obsidian. L'agent relit tout à la synchro suivante.
- Interface, modèles et noms de dossiers en allemand, anglais, français, italien, espagnol et roumain.

## 1. Installation

### Windows

1. Double-cliquez sur `Obsidian-Agent-Setup-2.0.0.exe`. Aucun droit d'administrateur n'est nécessaire.
2. Si « Windows a protégé votre ordinateur » s'affiche, cliquez sur **Informations complémentaires → Exécuter quand même**. L'installation n'est pas signée avec un certificat payant.
3. Choisissez la langue et suivez l'assistant.
4. L'installation configure ensuite automatiquement :
   - **Python**, s'il manque (via winget, sinon directement depuis python.org),
   - votre **coffre** (boîte de dialogue, éventuellement derrière la fenêtre),
   - le **démarrage automatique** en arrière-plan à chaque ouverture de session et la **synchro quotidienne**,
   - des raccourcis dans le **menu Démarrer** et sur le **Bureau**.
5. Le navigateur s'ouvre avec l'agent.

Dossier du programme : `%LOCALAPPDATA%\Programs\Obsidian-Agent` · Paramètres et base : `%LOCALAPPDATA%\Obsidian-Agent`

### macOS

1. Double-cliquez sur `Obsidian-Agent-2.0.0.pkg`.
2. Si macOS indique que le paquet ne peut pas être vérifié, choisissez **Réglages Système → Confidentialité et sécurité → Ouvrir quand même** (versions plus anciennes : clic droit sur le paquet → Ouvrir). Le paquet n'est pas signé avec un certificat de développeur Apple.
3. Suivez l'assistant et saisissez le mot de passe administrateur.
4. Après la copie, le paquet configure automatiquement : Python (depuis python.org, s'il manque), la langue de votre Mac, votre coffre (boîte de dialogue), le démarrage automatique et la synchro quotidienne.
5. Ouvrez ensuite l'agent via **Applications → Obsidian-Agent**.

Si le coffre se trouve dans *Documents*, sur le *Bureau* ou dans *iCloud Drive*, macOS peut bloquer la synchro en arrière-plan. Le paquet le détecte et affiche le fichier à ajouter dans **Réglages Système → Confidentialité et sécurité → Accès complet au disque**.

Programme : `/Applications/Obsidian-Agent` · Paramètres et base : `~/Library/Application Support/Obsidian-Agent` · Journal d'installation : `/tmp/obsidian-agent-install.log`

### Sans installation (tous systèmes)

Python 3.9 ou plus récent suffit. Décompressez le dossier `obsidian-agent` et lancez `start.bat` (Windows) ou `start.sh` (macOS/Linux). Flask est déjà inclus. Les paramètres sont alors enregistrés dans le dossier du programme. Pour la synchro quotidienne sous Linux, ajoutez `0 4 * * * cd /chemin/obsidian-agent && python3 agent.py sync --geplant` avec `crontab -e`.

## 2. Premiers pas

1. **Paramètres** : vérifiez le chemin du coffre, choisissez la langue.
2. **Équipe** : saisissez les membres avec nom et initiales.
3. **Projets** : créez un premier projet. La structure de dossiers ci-dessous est créée.
4. Créez des **tâches** et des documents de projet sous **Documents**.
5. Pour les réunions régulières, créez une série de **Réunions périodiques**.

## 3. Zones de l'interface

| Zone | Rôle |
|---|---|
| **Aujourd'hui** | Tâches du jour et en retard, échéances à venir, notes modifiées récemment, nouvelle tâche. |
| **Tâches** | Toutes les tâches par groupe, filtre par projet, terminer en un clic, changer le statut, reporter de « +1 jour ». |
| **Projets** | Créer des projets avec une structure fixe, compléter les projets incomplets. |
| **Documents** | Documents de projet à partir de modèles, placés automatiquement dans le bon dossier du projet. |
| **Depuis un modèle** | Nouvelle note à partir de n'importe quel modèle du dossier des modèles, y compris les vôtres. |
| **Réunions périodiques** | Séries de réunions avec fréquence, notes de réunion et actions. Chaque nouvelle réunion contient les actions ouvertes. |
| **Équipe** | Fiches avec rôle, contact, suppléant et les tâches ouvertes de chaque personne. |
| **Recherche** | Recherche plein texte dans tout le coffre. |
| **Paramètres** | Langue, chemin du coffre, noms de dossiers, heure de synchro, journal. |

Chaque titre est un lien `obsidian://` qui ouvre la note directement dans Obsidian.

## 4. Dossiers du coffre

| Dossier | Contenu |
|---|---|
| `Projets/` | Un sous-dossier par projet (structure ci-dessous) |
| `Taches/` | Tâches sans projet |
| `Notes/` | Documents sans projet |
| `_Modeles/` | Modèles, modifiables dans Obsidian |
| `Planning/` | Aperçu du jour et archives (automatique) |
| `Equipe/` | Une note par membre de l'équipe |
| `Reunions/` | Un sous-dossier par série avec réunions et actions |

## 5. Structure d'un projet

Chaque projet reçoit une note d'aperçu `_Projet_<Nom>.md` (objectifs, jalons, tâches ouvertes) et ces sous-dossiers, chacun avec un fichier `readme` :

| Dossier | Contenu |
|---|---|
| `01_Mandat_et_Contrats/` | Mandat de projet, offres, contrats, commandes et avenants. |
| `02_Parties_prenantes/` | Mandant, interlocuteurs, rôles, escalade et communication. |
| `03_Planification/` | Plan de projet, jalons, ressources, budget et décisions. |
| `04_Realisation/` | Livrables, concepts, documentation technique et tests. |
| `05_Risques_et_Changements/` | Risques, points ouverts et demandes de changement. |
| `06_Reporting/` | Rapports d'avancement, indicateurs et comité de pilotage. |
| `07_Proces-verbaux/` | Procès-verbaux, réunions périodiques et correspondance importante. |
| `08_Cloture/` | Réception, transfert à l'exploitation et retours d'expérience. |

« Compléter tous les projets » ajoute les dossiers manquants aux projets existants. Rien n'est jamais écrasé.

## 6. Documents de projet

| Document | Dossier | Nom de fichier |
|---|---|---|
| **Procès-verbal** | `07_Proces-verbaux/` | `YYYY-MM-DD_PV_….md` |
| **Décision** | `03_Planification/` | `Decision_YYYY-MM-DD_….md` |
| **Risque** | `05_Risques_et_Changements/` | `Risque_….md` |
| **Demande de changement** | `05_Risques_et_Changements/` | `Changement_YYYY-MM-DD_….md` |
| **Partie prenante / contact** | `02_Parties_prenantes/` | `Partie_prenante_….md` |
| **Rapport d'avancement** | `06_Reporting/` | `Rapport_YYYY-MM_….md` |
| **Clôture de projet** | `08_Cloture/` | `Cloture_….md` |

Créez aussi une tâche pour chaque action d'un procès-verbal afin qu'elle apparaisse sous Aujourd'hui et dans l'équipe.

## 7. Format des tâches

```markdown
---
typ: task
titel: Préparer le lancement
projekt: Migration M365
start: 2026-11-18
ende: 2026-11-20
status: offen            # offen | in_arbeit | wartend | erledigt
prioritaet: hoch         # hoch | mittel | niedrig
verantwortlich: AM       # nom ou initiales d'un membre de l'équipe
---
- [ ] Étape 1
- [x] Étape 2
```

- **Aujourd'hui** : début ≤ aujourd'hui ≤ fin · **En retard** : fin < aujourd'hui · **Planifiée** : début > aujourd'hui.
- Sans `status`, une tâche est considérée comme terminée lorsque toutes les cases sont cochées.
- Les noms des champs du frontmatter (`typ`, `titel`, `ende` = fin, `verantwortlich` = responsable …) sont identiques dans toutes les langues. L'agent peut ainsi lire n'importe quel coffre, même après un changement de langue.

## 8. Aperçu du jour et synchro

Chaque jour à 04:00 (réglable), l'agent lit toutes les notes et écrit l'aperçu du jour dans `Planning/Aujourdhui.md`, ainsi qu'une archive par jour. Vous voyez donc aussi l'aperçu dans Obsidian et sur votre téléphone. Si l'ordinateur était éteint, l'exécution est rattrapée. « Actualiser » lit le coffre immédiatement.

## 9. Changer de langue

En bas à gauche dans la navigation ou sous **Paramètres**. L'interface change immédiatement. Les nouveaux modèles sont créés dans la langue choisie. Dans un coffre sans projets, les noms de dossiers et la structure de projet sont aussi adaptés. Les dossiers et notes existants ne sont jamais renommés.

## 10. Adapter les modèles

Tous les modèles se trouvent dans le dossier des modèles du coffre et peuvent être modifiés dans Obsidian. Variables : `{{title}}`, `{{date}}`, `{{projekt}}`. Avec `zielordner: 03_…` dans le frontmatter d'un modèle personnalisé, vous définissez le dossier présélectionné. Les modèles standard supprimés sont recréés à la synchro suivante.

## 11. Facultatif : Dataview

Les aperçus de projet contiennent une requête Dataview des tâches ouvertes. Activez pour cela le plugin communautaire **Dataview** dans Obsidian. L'agent lui-même n'en a pas besoin.

## 12. Mise à jour, sauvegarde, désinstallation

- **Mise à jour** : installez simplement le nouveau programme d'installation ou paquet. Paramètres et base sont conservés.
- **Sauvegarde** : le coffre fait foi. La base ne contient en plus que l'historique quotidien.
- **Désinstallation Windows** : *Paramètres → Applications → Obsidian-Agent → Désinstaller*.
- **Désinstallation macOS** : *Applications → Obsidian-Agent → Désinstaller Obsidian-Agent*.
- Les deux sauvegardent `config.json` et `planer.db` dans un dossier `obsidian-agent-backup_<date>` sur le Bureau. **Votre coffre Obsidian n'est jamais modifié ni supprimé.**

## 13. Dépannage

| Problème | Solution |
|---|---|
| Le navigateur affiche « site inaccessible » | Ouvrez l'agent via le menu Démarrer / Applications. Journal : `logs/gui.log` dans le dossier des paramètres. |
| De nouvelles notes manquent dans l'interface | Cliquez sur « Actualiser ». Vérifiez le nom de fichier `Task_…` ou le champ `typ:`. |
| Une tâche n'apparaît pas chez un membre | Indiquez le nom complet ou les initiales de l'équipe dans le champ `verantwortlich`. |
| macOS : la synchro en arrière-plan échoue | Autorisez l'accès complet au disque pour le fichier Python indiqué (voir installation). |
| Le port 5055 est occupé | Modifiez `port` dans `config.json` et redémarrez l'agent. |

Ligne de commande : `python agent.py sync` · `python agent.py heute` (aujourd'hui) · `python agent.py projekt "Nom"` · `python agent.py info`

---
[Deutsch](Anleitung_DE.md) · [English](Guide_EN.md) · [Italiano](Guida_IT.md) · [Español](Guia_ES.md) · [Română](Ghid_RO.md)
