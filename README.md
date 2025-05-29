---
title: "beNetX – Semantische DotMesh Architektur"
owner: "system"
purpose: "Hauptdokumentation des beNetX-Systems, mit Fokus auf NoHouse.DotMesh"
created: "2025-05-20"
updated: "2025-05-28"
tags: ["documentation", "system", "technical-design", "architecture", "dotmesh", "supabase"]
status: "active"
---

# 🚀 beNetX System

## 📋 Übersicht

beNetX ist ein modulares, verteiltes Systemkonzept für intelligente Datenverarbeitung und Automatisierung. Es dient als Dach für verschiedene datenzentrierte Komponenten und Projekte.

### Kernidee Module (Vision)
- **benet-control**: Zentrale Steuerung und Orchestrierung
- **benet-dots**: Dokumentations- und Tracking-System (Basis für NoHouse.DotMesh)
- **benet-front**: Benutzeroberfläche
- **benet-jobs**: Job-Management und -Ausführung
- **benet-ml**: Machine Learning Komponenten
- **benet-sync**: Daten-Synchronisation (realisiert in NoHouse.DotMesh)
- **benet-results**: Ergebnisverarbeitung
- **benet-dashboard**: Visualisierung und Monitoring

---

# NoHouse.DotMesh powered by beNetX

## 🎯 Ziel & Funktion

**NoHouse.DotMesh** ist die erste Kernimplementierung im beNetX Ökosystem. Es ist ein verteiltes Dot-Management-System, das die Erfassung, Verwaltung und Synchronisation von granularen Informationseinheiten ("Dots") über verschiedene Systeme hinweg ermöglicht, inklusive einer robusten Synchronisation mit Supabase als Backend-Speicher.

### Hauptmerkmale
- Erstellung und Verwaltung von "Dots" (atomare Informationseinheiten mit Metadaten und Daten-Layern).
- Automatische Synchronisation von Dots mit einer Supabase-Datenbank.
- Strukturierte Metadaten-Extraktion aus Dateinamen und YAML-Dateien.
- Konfigurierbare Payloads für verschiedene Supabase-Tabellen (`products_echo`, `curation_queue`, `product_texts`).
- Integritätsprüfungen und Logging.

## 🛠️ Technologie-Stack (für NoHouse.DotMesh)

- **Scripting/Backend**: Python
- **Datenbank (Backend-Synchronisation)**: Supabase (PostgreSQL)
- **Datenformat**: YAML (für Metadaten), diverse (für Daten-Layer)

## 📦 Installation & Setup (für NoHouse.DotMesh)

1.  **Repository klonen**:
    ```bash
    git clone https://github.com/beNetX/github.git
    cd github/NoHouse-DotMesh 
    # Oder je nachdem, wo sich NoHouse-DotMesh innerhalb des Repos befindet.
    # Ggf. ist das Haupt-Repo direkt NoHouse-DotMesh, dann nur:
    # cd github
    ```

2.  **Virtual Environment erstellen und aktivieren**:
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    ```

3.  **Abhängigkeiten installieren**:
    Stellen Sie sicher, dass alle notwendigen Python-Pakete installiert sind. Diese sind in `NoHouse-DotMesh/bridge/requirements.txt` (oder einem ähnlichen Pfad) zu finden.
    ```bash
    pip install -r NoHouse-DotMesh/bridge/requirements.txt 
    # (Pfad ggf. anpassen)
    # Benötigte Pakete beinhalten typischerweise: requests, python-dotenv, PyYAML
    ```

4.  **Umgebungsvariablen setzen**:
    Erstellen Sie eine `.env`-Datei im `NoHouse-DotMesh/bridge` Verzeichnis (oder wo `sync_to_supabase.py` liegt) mit folgendem Inhalt:
    ```env
    SUPA_URL="DEINE_SUPABASE_URL_MIT_TRAILNG_SLASH/"
    SUPA_KEY="DEIN_SUPABASE_SERVICE_ROLE_KEY" 
    # WICHTIG: Benutzen Sie den service_role key für Backend-Skripte!
    LOG_LEVEL="INFO" # oder DEBUG für mehr Details
    # Weitere spezifische Variablen nach Bedarf
    ```

## ⚙️ Nutzung

Der Hauptprozess für die Synchronisation mit Supabase wird durch das Skript `sync_to_supabase.py` gesteuert.

1.  **Dots vorbereiten**:
    Stellen Sie sicher, dass Ihre Dots im konfigurierten Quellverzeichnis (`source_dots_local` oder ähnlich) liegen und die korrekte Struktur haben (siehe "Dot-Struktur").

2.  **Synchronisationsskript ausführen**:
    ```bash
    python NoHouse-DotMesh/bridge/sync_to_supabase.py --verbose
    # (Pfad zum Skript ggf. anpassen)
    ```
    Das Skript verarbeitet die Dots und synchronisiert sie mit den entsprechenden Tabellen in Supabase.

### Dot-Struktur

Ein "Dot" ist ein Verzeichnis, das typischerweise wie folgt aufgebaut ist:

```
mein_spezifischer_dot_name_JJJJMMTT_HHMMSS.dot/
├── meta/
│   └── meta_typ_untertyp_JJJJMMTT_HHMMSS.yaml
└── layer/
    └── beliebige_daten_datei.endung
```

**`meta_typ_untertyp_JJJJMMTT_HHMMSS.yaml`**:
- Enthält Metadaten zum Dot. Wichtige Felder, die von `sync_to_supabase.py` erwartet werden können (Beispiele):
    - `dot_id`: Eindeutige ID des Dots (wird oft aus dem Dot-Verzeichnisnamen extrahiert).
    - `dot_type`: Typ des Dots (z.B. `product`, `echo`, `rawdata`).
    - `origin_node`: Herkunft des Dots (z.B. `w4y`, `notion`).
    - `text_type`: Spezifischer Typ von Textdaten (z.B. `short_summary`, `echo_positive`).
    - `created_at`, `updated_at`: Zeitstempel (können aus Dateinamen oder Metadaten gelesen werden).
    - Weitere für die jeweiligen Supabase-Tabellen relevante Felder.
- Der Zeitstempel im Dateinamen der Meta-Datei und des Dot-Ordners ist oft entscheidend für `created_at`/`updated_at`.

**`layer/` Verzeichnis**:
- Enthält die eigentlichen Nutzdaten des Dots (Texte, Bilder, strukturierte Daten etc.).
- Die Verarbeitung dieser Dateien hängt von der Implementierung im `sync_to_supabase.py` Skript ab.

## 🔄 Synchronisationslogik mit Supabase

Das `sync_to_supabase.py` Skript:
1.  Durchsucht das Quellverzeichnis nach Dots.
2.  Extrahiert Metadaten aus den Dot-Verzeichnisnamen und den `meta.yaml` Dateien.
3.  Transformiert diese Metadaten in Payloads für die Supabase-Tabellen:
    *   `products_echo`
    *   `curation_queue`
    *   `product_texts`
4.  Verwendet Hilfsfunktionen (`safe_get_float`, `safe_get_bool`, `get_valid_source`, `get_valid_text_type`, etc.), um Datentypen zu validieren und zu konvertieren und Check-Constraints von Supabase einzuhalten.
5.  Sendet die Daten per HTTP POST Request an die Supabase API (`/rest/v1/`).
6.  Behandelt Fehler und loggt den Prozess.

**Wichtige Hinweise für Supabase:**
- **RLS Policies**: Müssen direkt in der Supabase SQL-Konsole eingerichtet werden, da DDL-Befehle nicht über die REST-API ausgeführt werden können.
- **Spalten**: Stellen Sie sicher, dass alle Spalten, die vom Skript befüllt werden, in den Supabase-Tabellen existieren und die korrekten Datentypen haben (z.B. `TEXT` statt `UUID` für IDs, wenn diese nicht als UUIDs generiert werden).
- **Constraints**: `NOT NULL` Constraints ohne `DEFAULT` Werte in Supabase können zu Fehlern führen, wenn die Dot-Metadaten nicht immer alle erforderlichen Felder liefern. Überprüfen Sie `CHECK` Constraints (z.B. für `source`, `text_type`) und stellen Sie sicher, dass die Dots valide Werte liefern oder die Tabellendefinition angepasst wird.

## 🪵 Logging & Monitoring

- Das `sync_to_supabase.py` Skript nutzt das Python `logging` Modul.
- Die Ausgabe erfolgt in die Konsole und optional in Logdateien, abhängig von der Konfiguration.
- Der `LOG_LEVEL` in der `.env` Datei steuert die Detailtiefe der Logs.
- Überprüfen Sie die Konsolenausgabe auf Fehlermeldungen (`400 Bad Request`, `401 Unauthorized`, `Constraint violations`, etc.).

## 🧪 Tests (Beispielhaft)

```bash
# Unit Tests (falls vorhanden)
# pytest

# Manuelle Tests
# 1. Einen neuen Dot im Quellverzeichnis erstellen.
# 2. sync_to_supabase.py ausführen.
# 3. Daten in Supabase überprüfen.
```

## 📚 Weitere Dokumentation (Beispiele)

- Detailliertere Systemarchitektur: `benet-docs/docs/system/architecture.md`
- API-Dokumentation (falls vorhanden): `benet-docs/docs/api/overview.md`
- Werte und Prinzipien: `benet-docs/docs/werte_lizenzen_richtlinien/werteanspruch_benetx_dot_oekosystem_v1.0.md`

## 🤝 Beitragen

1.  Fork des Repositories `https://github.com/beNetX/github.git` erstellen.
2.  Feature Branch erstellen (`git checkout -b feature/AmazingFeature`).
3.  Änderungen committen (`git commit -m 'Add some AmazingFeature'`).
4.  Branch pushen (`git push origin feature/AmazingFeature`).
5.  Pull Request erstellen.

## 📜 Lizenz & Urheberschaft

Dieses Projekt und seine Komponenten unterliegen, sofern nicht anders im jeweiligen Unterverzeichnis oder der Datei spezifiziert, der Lizenz **CC BY-NC-SA 4.0**.  
Der Projektstart und die Kernarchitektur sind durch ein signiertes Urheberdokument belegt. Details finden Sie in `LICENSE.md` und `COPYRIGHT.md`.

[Zur Lizenzbeschreibung (CC BY-NC-SA 4.0) »](https://creativecommons.org/licenses/by-nc-sa/4.0/)

<a href="https://beNetX.com">beNetX</a> © 2025 by <a href="https://benatzky.at">Moritz Oliver Benatzky</a> is licensed under 
<a href="https://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International</a>
<img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;"></img>
<img src="https://mirrors.creativecommons.org/presskit/icons/by.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;"></img>
<img src="https://mirrors.creativecommons.org/presskit/icons/nc.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;"></img>
<img src="https://mirrors.creativecommons.org/presskit/icons/sa.svg" style="max-width: 1em;max-height:1em;margin-left: .2em;"></img>
