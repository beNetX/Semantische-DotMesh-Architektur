<!-- SPDX-License-Identifier: LicenseRef-SinnZeit-1.0 -->
<!-- SPDX-FileCopyrightText: 2025 beNetX – Moritz Oliver Benatzky -->
<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky -->

<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky et al. -->

<!-- Copyright © 2025 beNetX – Moritz Oliver Benatzky et al. -->


---
title: "beNetX Projektstruktur"
owner: "system"
purpose: "Übersicht der beNetX-Module und deren Funktionen"
created: "2024-03-20"
tags: ["documentation", "system", "architecture", "structure"]
status: "active"
---

# beNetX Projektstruktur

## Hauptmodule

### Core-Module
- `benetx-control/` - Zentrale Steuerung und Orchestrierung
- `benetx-dashboard/` - Web-basiertes Dashboard für Monitoring und Steuerung
- `benetx-docs/` - Systemdokumentation und Wissensbasis
- `benetx-dots/` - Dot-System für Datenverwaltung und -strukturierung
- `benetx-echo/` - Echo & Resonanz Semilogie-Implementierung
- `benetx-front/` - Frontend-Anwendung
- `benetx-gateways/` - API-Gateways für externe Dienste
- `benetx-jobs/` - Hintergrund-Jobs und Automatisierung
- `benetx-llm/` - LLM-Integration (Mistral via Ollama)
- `benetx-ml/` - Machine Learning Komponenten
- `benetx-results/` - Ergebnisverarbeitung und -speicherung
- `benetx-sync/` - Synchronisation zwischen Systemen

## Modul-Details

### benetx-control
- Zentrale Steuerung des Gesamtsystems
- Job-Orchestrierung
- System-Monitoring
- Konfigurationsmanagement

### benetx-dashboard
- Web-basiertes Dashboard
- Echtzeit-Monitoring
- System-Status
- Benutzer-Interface

### benetx-docs
- Systemdokumentation
- API-Dokumentation
- Entwickler-Guides
- Architektur-Dokumentation

### benetx-dots
- Dot-System Implementierung
- Datenstruktur-Definitionen
- Dot-Verarbeitung
- Dot-Speicherung

### benetx-echo
- Echo & Resonanz Semilogie
- Text-Generierung
- Semantische Analyse
- Empfehlungslogik

### benetx-front
- Frontend-Anwendung
- Benutzer-Interface
- Interaktive Komponenten
- API-Integration

### benetx-gateways
- Notion Gateway
- Airtable Gateway
- Google Services Gateway
- Weitere API-Integrationen

### benetx-jobs
- Hintergrund-Jobs
- Automatisierte Tasks
- Batch-Verarbeitung
- Scheduling

### benetx-llm
- LLM-Integration
- Mistral via Ollama
- Text-Generierung
- Prompt-Engineering

### benetx-ml
- Machine Learning Modelle
- MatrixScore Berechnung
- Feature Engineering
- Modell-Training

### benetx-results
- Ergebnisverarbeitung
- Daten-Export
- Berichtsgenerierung
- Ergebnis-Speicherung

### benetx-sync
- Daten-Synchronisation
- System-Integration
- Echtzeit-Updates
- Konflikt-Lösung

## Verzeichnisstruktur

```
beNetX/
├── benetx-control/          # Zentrale Steuerung
├── benetx-dashboard/        # Web-Dashboard
├── benetx-docs/            # Systemdokumentation
│   └── docs/              # Dokumentationsdateien
├── benetx-dots/            # Dot-System
│   └── dots/              # Dot-Dateien
├── benetx-echo/            # Echo & Resonanz
├── benetx-front/           # Frontend
├── benetx-gateways/        # API-Gateways
├── benetx-jobs/            # Hintergrund-Jobs
├── benetx-llm/             # LLM-Integration
│   └── prompts/           # LLM-Prompts
├── benetx-ml/              # Machine Learning
├── benetx-results/         # Ergebnisse
└── benetx-sync/            # Synchronisation
```

## Entwicklungsumgebung

- **Lokale Entwicklung:** Mac Mini
- **Produktion:** be-hpworker
- **Version Control:** Git
- **Python Environment:** venv
- **Node.js Environment:** npm/yarn

## Wichtige Dateien

- `README.md` - Hauptdokumentation
- `.gitignore` - Git-Ausschlussregeln
- `requirements.txt` - Python-Abhängigkeiten
- `package.json` - Node.js-Abhängigkeiten
- `config_*.json` - Modulspezifische Konfigurationen 