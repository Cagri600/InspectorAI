# Projektfunktionen und technische Leistungen

| Nachweisbare Leistung | Konkrete Umsetzung | Seriöse Portfolio-Aussage |
|---|---|---|
| Native Windows-Oberfläche | MainForm, ModernHomePanel, SectionTabs, AppTheme, eigengezeichnete Steuerelemente | Desktop-UI mit konsistenter Navigation und gezielten DPI-Korrekturen |
| Echte Systemdaten | Win32-CPU/RAM, WMI, Ereignisprotokolle, DriveInfo, Registry, nvidia-smi | Mehrere Windows-Datenquellen zu einem lesenden Check integriert |
| Robuste asynchrone Abläufe | CancellationToken, SemaphoreSlim, Fristen und isolierte Probeprozesse | UI und Sammler gegen Hänger, parallele Scans und späte Ergebnisse abgesichert |
| Nachvollziehbare Diagnose | StructuredDiagnosis, ScanCoverageRules, HealthPolicy | Messbelege, Unsicherheit und Quellenabdeckung statt unbegründeter Defektbehauptungen |
| Lokale KI-Integration | OllamaLocalClient, BundledAi, Qwen2.5:1.5b | Bestehendes Sprachmodell lokal integriert; kein selbst trainiertes Modell |
| Begrenzte KI-Ausgaben | Befund-ID-Auswahl, Schema-/Frischeprüfung, AiOutputPolicy | KI-Erklärung von Systemberechtigungen und Reparaturausführung getrennt |
| Chat-Bedienung | LocalChatForm, aktueller Fragenkontext und Abbruchpfade | Folgefragen, Anfragewechsel und sichere lesende Werkzeuge umgesetzt |
| Datenhaltung und Export | JSON-Einstellungen, Verlauf, anonyme Exportverträge | Lokale Speicherung und überprüfbare Berichtsformate integriert |
| Sicherheitsgrenzen | Fester Katalog, Worker, Vorgangskennungen, Locks und feste Sperre | Systemänderungen nicht ungeprüft freigeschaltet |
| Windows-Paketierung | Self-contained Publish, Inno Setup, SHA-256, gebündelte KI | Offline-Verteilung mit dokumentierten Test- und Signierungsgrenzen vorbereitet |
| Qualitätsarbeit | Regeltests, Transporttests, native Windows- und GUI-Prüfungen | Konkrete Fehler anhand nachvollziehbarer Regressionen bearbeitet |

## Nicht als eigene oder aktive Leistung behaupten

Kein eigenes Training von Qwen/Ollama; kein selbst entwickeltes Betriebssystem oder Hardwaretreiber; keine autonome Reparatur aller Windows-Probleme; kein nachgewiesener Unternehmens-Rollout; keine vollständige Misch-DPI-/Fremd-PC-Abnahme; keine garantierte KI-Korrektheit; keine belegte aktuelle grüne GitHub-CI.

## Bewerbungstext zur persönlichen Prüfung

„InspectorAI ist mein Praxisprojekt für lokale Windows-Diagnose mit integrierter Offline-KI. Das Projekt verbindet eine native C#-/WinForms-Oberfläche mit Windows-Messquellen, nachvollziehbaren Diagnoseregeln und einer begrenzten Ollama-/Qwen-Auswertung. Ein Schwerpunkt lag auf Fehlerbehandlung, Abbruch, Datenfrische und sicheren Prozessgrenzen. Die private Testausgabe wird mit selbstständiger Windows-Laufzeit und dokumentierten Prüfnachweisen verteilt.“

Vor Verwendung persönliche Rolle und KI-Unterstützung ergänzen. Die Implementierung belegt Projektfähigkeiten; sie belegt allein nicht, welche Codezeile der Projektinhaber ohne Unterstützung geschrieben hat.
