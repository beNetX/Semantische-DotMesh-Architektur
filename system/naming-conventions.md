<!-- SPDX-License-Identifier: LicenseRef-SinnZeit-1.0 -->
<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky et al. -->

---
title: "beNetX Namenskonventionen"
owner: "system"
purpose: "Dokumentation der Namenskonventionen im beNetX-System"
created: "2025-05-13"
tags: ["documentation", "system", "naming", "conventions", "technical-design"]
status: "active"
---

# 📝 Namens- und Tag-Konventionen

## 📄 Markdown-Dateinamen

### Haupt-Readme-Dateien
- Dateiname: `README.md` (großgeschrieben)
- Verwendung: Für Hauptdokumentationen von Modulen/Projekten
- Beispiel: `benet-docs/README.md`

### Dokumentationsdateien
- Dateiname: Kleinschreibung, Wörter mit Bindestrich verbunden
- Format: `beispiel-datei.md`
- Beispiele:
  - `technische-vision.md`
  - `dotfs-konzept.md`
  - `system-architektur.md`

## 🐍 Python-Dateinamen

- Dateiname: Kleinschreibung, Wörter mit Unterstrich verbunden (Snake-Case)
- Format: `beispiel_datei.py`
- Beispiele:
  - `doc_index_generator.py`
  - `sync_all_nodes.sh`
  - `process_dots.py`

## 🏷️ Tags im YAML-Header

### Allgemeine Regeln
- Primär Kleinschreibung
- Mehrteilige Begriffe mit Bindestrich verbunden
- Eigennamen/Akronyme nach Bedarf

### Beispiele
```yaml
tags: [
    "benetx-vision",
    "technische-vision",
    "dot-fs",
    "gpt",
    "xgboost",
    "system-documentation"
]
```

### Kategorien
1. **System-Tags**
   - `system`
   - `documentation`
   - `naming-conventions`
   - `style-guide`

2. **Technologie-Tags**
   - `python`
   - `markdown`
   - `yaml`
   - `dot-fs`

3. **Projekt-Tags**
   - `benetx-vision`
   - `technical-design`
   - `architecture`

## 📌 Best Practices

1. **Konsistenz**
   - Halte dich strikt an die definierten Konventionen
   - Verwende die gleichen Tags für ähnliche Dokumente

2. **Lesbarkeit**
   - Wähle beschreibende Namen
   - Vermeide Abkürzungen, außer sie sind allgemein üblich

3. **Wartbarkeit**
   - Dokumentiere neue Tags im System
   - Prüfe regelmäßig auf veraltete oder redundante Tags

## 🔄 Änderungshistorie

- 2024-03-20: Erste Version der Konventionen
- 2024-03-20: Hinzufügung von Best Practices und Kategorien 