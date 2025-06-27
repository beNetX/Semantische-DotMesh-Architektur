<!-- SPDX-License-Identifier: CC-BY-NC-SA-4.0 -->
<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky et al. -->

<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky et al. -->


---
title: "beNetX Hybrid-Dokumentationssystem"
owner: "system"
purpose: "Konzeption des hybriden Dokumentationssystems"
created: "2025-05-13"
tags: ["documentation", "system", "hybrid-docs", "technical-design", "architecture"]
status: "active"
---

# 🧠 Prompt: beNetX HybridDocSystem + GitHub-Anbindung

## 🎯 Ziel

Ich möchte ein semantisch selbstreflektierendes, hybrid organisiertes Dokumentationssystem für mein beNetX-Projekt.  
Die `.md`-Dateien enthalten YAML-Header (inkl. `owner`, `purpose`, `status`) und liegen thematisch organisiert im `docs/` Ordner.  
Ein zentrales `index.yaml` (im Ordner `benet-docs/`) referenziert alle aktiven Dokumente.  
Dieses System soll mit einem privaten **GitHub-Repo** verbunden und versioniert werden.

---

## ✅ Schritte zur Umsetzung

### 1. 📁 Struktur erstellen

- Thematische Unterordner im `docs/` Ordner (z.B. `docs/system/`, `docs/dotfs/`)
- `benet-docs/index.yaml` mit YAML-Metadaten für alle aktiven `.md`-Dateien

### 2. ✍️ Markdown-Template definieren

- YAML-Header pro Datei:
```yaml
---
title: Beispieltitel
owner: be-pi2
purpose: Modulbeschreibung
created: 2024-03-20
tags: [system, concept, documentation]
status: active
---
```

### 3. 🔁 Index-Generator (`doc_index_generator.py`)

- durchsucht den `docs/` Ordner rekursiv nach `.md` Dateien
- erzeugt/aktualisiert `index.yaml` mit Metadaten

### 4. 🧩 Dot-Erzeugung (`doc_to_dot.py`)

- für jedes `.md` mit `status: active` wird ein `dot_doc_*.json` erzeugt
- Dots werden im `dots/` Ordner gespeichert

### 5. 🐙 GitHub-Anbindung

- Repository `benet-docs` auf GitHub anlegen
- `git init`, `git remote add origin <repo-url>`
- `.gitignore`, `README.md` hinzufügen

### 6. 🔄 Commit-Monitoring (optional)

- jedes `git commit` erzeugt einen Dot (`dot_commit_*.json`)
- Felder: `files changed`, `author`, `message`, `timestamp`

### 7. 📤 Push/Sync-Skript (`git_sync_docs.sh`)

- automatischer `git add`, `commit`, `push` bei Änderungen

### 8. 🖇️ Optional: GitHub Pages

- öffentliches Dokumentationsportal aktivieren (Markdown gerendert)

---

## 💡 Zusatzziele (optional)

- CLI: `benet-doc new <thema> <titel>` → erstellt `.md` mit YAML-Kopf
- Cronjob: regelmäßig `doc_index_generator.py && doc_to_dot.py`
- Notion-Sync: `index.yaml` als JSON in Notion importieren

---

## 📁 Aktuelle Struktur

```
benet-docs/
├── README.md
├── index.yaml
├── doc_index_generator.py
├── doc_to_dot.py
├── git_sync_docs.sh
└── docs/
    ├── dotfs/
    │   └── ram_logging.md
    └── system/
        └── hybriddocsystem_konzeption.md
```

🧠 Zielsystem: Dokumentation, die sich selbst kennt, verändert und verlinkt.  
Bitte beginne mit dem Index-Generator, dann Dot-Sync, anschließend GitHub-Verknüpfung.
