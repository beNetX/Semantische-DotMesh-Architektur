<!-- SPDX-License-Identifier: CC-BY-NC-SA-4.0 -->
<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky et al. -->

<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky et al. -->


---
title: "beNetX Dot System"
owner: "system"
purpose: "Dokumentation des beNetX Dot-Systems für semantische Datenverarbeitung"
created: "2025-05-20"
tags: ["documentation", "system", "dots", "semantic", "technical-design", "architecture"]
status: "active"
---

# 🔄 beNetX Dot System

## 📋 Übersicht

Das beNetX Dot System ist die zentrale Komponente für semantische Datenverarbeitung im beNetX-Ökosystem. Es ermöglicht die Erstellung, Verwaltung und Verknüpfung von semantischen Einheiten (Dots) aus verschiedenen Quellen.

## 🏗️ Architektur

### Kern-Komponenten

1. **Dot Generator**
   - Erstellt Dots aus verschiedenen Quellen
   - Implementiert Hash-basierte Änderungserkennung
   - Unterstützt atomare Updates

2. **Dot Store**
   - Speichert Dots in JSON-Format
   - Implementiert Status-Views via Symlinks
   - Garantiert atomare Schreiboperationen

3. **Dot Processor**
   - Verarbeitet Dots für verschiedene Anwendungsfälle
   - Implementiert Lifecycle-Tracking
   - Unterstützt In-Place Updates

### Technologie-Stack

- Python 3.11+
- JSON für Dot-Speicherung
- ULID für eindeutige Identifikation
- MD5 für Content-Hashing
- Symlinks für Status-Views

## 🚀 Features

### Dot-Struktur

```json
{
  "dot-id": "dot-doc-control-01JVPMHHSQW3VMKNDJ0Y2QDCY1",
  "dot-type": "documentation",
  "created-at": "2025-05-20T10:29:35.973283Z",
  "status": "valid",
  "lifecycle": [
    {
      "event": "birth",
      "ts": "2025-05-20T10:29:35Z",
      "source": "doc-to-dot-processor.py"
    }
  ],
  "module": "benet-control",
  "title": "beNetX Control Entwickler-Dokumentation",
  "purpose": "Technische Dokumentation für Entwickler des Control-Moduls",
  "tags": ["documentation", "system", "control", "development", "technical-design"],
  "relative-path": "benet-control/developer-control.md",
  "filename": "developer-control.md",
  "metadata": {
    "created-at-doc": "2025-05-12",
    "last-modified-doc-fs-at": "2025-05-20T11:44:44Z"
  },
  "content-hash-md": "9a447338f481cc0000447491fabafd42"
}
```

### Optimierungen

1. **Minimale Schreiblast**
   - Hash-basierte Änderungserkennung
   - Nur notwendige Updates
   - Atomare Schreiboperationen

2. **Stabile Referenzen**
   - ULID-basierte Dot-IDs
   - Ein Dot pro Dokument
   - In-Place Updates

3. **Vollständige Historie**
   - Lifecycle-Tracking
   - Event-basierte Änderungsprotokollierung
   - Status-Views

## 🛠️ Implementation

### Dot Generator

```python
def upsert-dot(dot-path: Path, new-payload: dict, new-hash: str, now-iso: str):
    if dot-path.exists():
        # Update existierender Dot
        with dot-path.open() as f:
            dot = json.load(f)

        if dot["content-hash-md"] == new-hash:
            return "unchanged"

        dot["content-hash-md"] = new-hash
        dot["status"] = "valid"
        dot["lifecycle"].append({
            "event": "content-updated",
            "ts": now-iso.split('.')[0] + 'Z',
            "hash": new-hash
        })
    else:
        # Erstelle neuen Dot
        dot = {
            "dot-id": dot-path.stem,
            "dot-type": "documentation",
            "created-at": now-iso,
            "status": "valid",
            "lifecycle": [{
                "event": "birth",
                "ts": now-iso.split('.')[0] + 'Z',
                "source": "doc-to-dot-processor.py"
            }],
            "content-hash-md": new-hash,
            **new-payload
        }

    # Atomares Schreiben
    tmp = dot-path.with-suffix(".tmp")
    with tmp.open("w") as f:
        json.dump(dot, f, indent=2)
    tmp.replace(dot-path)
    return "updated" if dot-path.exists() else "created"
```

### Status-Views

```python
def refresh-symlink(dot-path: Path, new-status: str):
    link-root = Path(DOT-ROOT, "status-views")
    for d in link-root.iterdir():
        link = d / dot-path.name
        if link.is-symlink():
            link.unlink()
    new-dir = link-root / new-status
    new-dir.mkdir(parents=True, exist-ok=True)
    (new-dir / dot-path.name).symlink-to(
        os.path.relpath(dot-path, new-dir))
```

## 📈 Vorteile

1. **Effizienz**
   - Minimale Schreiboperationen
   - Atomare Updates
   - Hash-basierte Optimierung

2. **Zuverlässigkeit**
   - Stabile Referenzen
   - Crash-sichere Updates
   - Vollständige Historie

3. **Flexibilität**
   - Status-Views
   - Lifecycle-Tracking
   - Erweiterbare Struktur

## 🔒 Sicherheit

### Best Practices

1. **Atomare Operationen**
   - Temp-File + rename
   - Crash-sichere Updates
   - Konsistente Zustände

2. **Validierung**
   - Hash-basierte Integritätsprüfung
   - Schema-Validierung
   - Status-Tracking

3. **Audit**
   - Lifecycle-Events
   - Änderungshistorie
   - Status-Views

## 📝 Changelog

### v1.0.0 (2025-05-20)
- Initiale Version
- Dot-Generator
- Status-Views
- Lifecycle-Tracking

## 📄 Lizenz

Dieses Projekt ist unter der MIT-Lizenz lizenziert - siehe [LICENSE.md](LICENSE.md) für Details. 
