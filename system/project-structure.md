<!-- SPDX-License-Identifier: LicenseRef-SinnZeit-1.0 -->
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
- `benet-control/` - Zentrale Steuerung und Orchestrierung
- `benet-dashboard/` - Web-basiertes Dashboard für Monitoring und Steuerung
- `benet-docs/` - Systemdokumentation und Wissensbasis
- `benet-dots/` - Dot-System für Datenverwaltung und -strukturierung
- `benet-echo/` - Echo & Resonanz Semilogie-Implementierung
- `benet-front/` - Frontend-Anwendung
- `benet-gateways/` - API-Gateways für externe Dienste
- `benet-jobs/` - Hintergrund-Jobs und Automatisierung
- `benet-llm/` - LLM-Integration (Mistral via Ollama)
- `benet-ml/` - Machine Learning Komponenten
- `benet-results/` - Ergebnisverarbeitung und -speicherung
- `benet-sync/` - Synchronisation zwischen Systemen

## Modul-Details

### benet-control
- Zentrale Steuerung des Gesamtsystems
- Job-Orchestrierung
- System-Monitoring
- Konfigurationsmanagement

### benet-dashboard
- Web-basiertes Dashboard
- Echtzeit-Monitoring
- System-Status
- Benutzer-Interface

### benet-docs
- Systemdokumentation
- API-Dokumentation
- Entwickler-Guides
- Architektur-Dokumentation

### benet-dots
- Dot-System Implementierung
- Datenstruktur-Definitionen
- Dot-Verarbeitung
- Dot-Speicherung

### benet-echo
- Echo & Resonanz Semilogie
- Text-Generierung
- Semantische Analyse
- Empfehlungslogik

### benet-front
- Frontend-Anwendung
- Benutzer-Interface
- Interaktive Komponenten
- API-Integration

### benet-gateways
- Notion Gateway
- Airtable Gateway
- Google Services Gateway
- Weitere API-Integrationen

### benet-jobs
- Hintergrund-Jobs
- Automatisierte Tasks
- Batch-Verarbeitung
- Scheduling

### benet-llm
- LLM-Integration
- Mistral via Ollama
- Text-Generierung
- Prompt-Engineering

### benet-ml
- Machine Learning Modelle
- MatrixScore Berechnung
- Feature Engineering
- Modell-Training

### benet-results
- Ergebnisverarbeitung
- Daten-Export
- Berichtsgenerierung
- Ergebnis-Speicherung

### benet-sync
- Daten-Synchronisation
- System-Integration
- Echtzeit-Updates
- Konflikt-Lösung

## Verzeichnisstruktur

```
beNetX/
├── benet-control/          # Zentrale Steuerung
├── benet-dashboard/        # Web-Dashboard
├── benet-docs/            # Systemdokumentation
│   └── docs/              # Dokumentationsdateien
├── benet-dots/            # Dot-System
│   └── dots/              # Dot-Dateien
├── benet-echo/            # Echo & Resonanz
├── benet-front/           # Frontend
├── benet-gateways/        # API-Gateways
├── benet-jobs/            # Hintergrund-Jobs
├── benet-llm/             # LLM-Integration
│   └── prompts/           # LLM-Prompts
├── benet-ml/              # Machine Learning
├── benet-results/         # Ergebnisse
└── benet-sync/            # Synchronisation
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