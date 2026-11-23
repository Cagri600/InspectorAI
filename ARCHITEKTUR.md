# Architektur

## Projektgrenzen

| Projekt | Verantwortung |
|---|---|
| `src/Inspector.Desktop.Windows` | WinForms-Shell, Seiten, Sammler, KI-Transport, lokale Speicherung und Prozesskoordination |
| `src/InspectorAI.Diagnostics` | Datenträger für zeitgebundene Messbelege, deterministische Diagnoseregeln und strukturierte Befunde; kein Sensor-/Shell-/HTTP-Zugriff in der Regelbibliothek |
| `src/InspectorAI.RepairWorker` | Separater CLI-Prozess für einen festen Aktionskatalog; systemändernde Ausführung in der privaten Ausgabe blockiert |
| `tests/*` | Eigene ausführbare .NET-Testprogramme; zusätzlich Python-/PowerShell-Verifikationen |

Die Desktop-App referenziert die Diagnostikbibliothek. Der Worker bindet ausgewählte Sicherheits-/Katalogdateien über `Compile Include ... Link` ein. Es gibt keinen nachgewiesenen MVVM-Stack, keinen Dependency-Injection-Container und keine Datenbank.

## Weg einer Diagnose

1. `MainForm` navigiert zwischen eingebetteten Forms; `ModernHomePanel` zeigt aktuelle Ressourcen und startet den Check.
2. `ReadOnlyHealthScan` koordiniert sechs unabhängige Quellen. Ein `SemaphoreSlim` verhindert konkurrierende Gesamtscans; `CancellationToken`, `WaitAsync` und `ScanTaskPolicy` begrenzen die Wartezeit.
3. Hardware/WMI und Windows-Ereignisse werden über `IsolatedHardwareProbe` und `IsolatedEventProbe` in eigenen Prozessen gelesen. Run-ID und Ergebnisvalidierung begrenzen die Übernahme fremder, ungültiger oder veralteter Ergebnisse.
4. Sammler liefern Messwerte mit Zeitpunkten und Quellenabdeckung. Regeln unterscheiden Messbefund, mögliche Ursache und fehlende Daten. Der vollständige Check ist keine Garantie vollständiger Systemgesundheit.
5. `SimpleCheckForm` und die Befund-/Expertenansichten zeigen Erklärung und passende lesende Untersuchung. Eine Empfehlung löst nicht automatisch eine Änderung aus.

## KI-Grenze

`BundledAi` startet die enthaltene Ollama-EXE mit eigenem Modellverzeichnis, Loopback-Bindung und Prozesslebenszyklus. Ein Windows-Jobobjekt dient der Begrenzung eigener Kindprozesse. `OllamaLocalClient` und `OllamaDiagnosticService` kommunizieren per HTTP/JSON mit dem lokalen Dienst.

`PcAssistantContext` ordnet die aktuelle Frage den passenden aktuellen Messbelegen zu. Die strukturierte Modellantwort darf vorhandene Befund-IDs auswählen oder sich enthalten. Schema, Frische und erlaubte IDs werden geprüft. `StructuredDiagnosisPanel` stellt Originalbelege und Auswahl getrennt dar. Das Modell ist keine unabhängige Messquelle.

`LocalChatForm` verwaltet Senden, Folgefragen, Abbruch und Anfragewechsel. Allgemeiner freier Chat ist von messdatengebundener Einordnung zu unterscheiden. Eine eng begrenzte fachliche SSD-Korrektur wird ausdrücklich als geprüfte Wissensgrundlage gekennzeichnet, nicht als neue Modellantwort.

## Speicherung und Verteilung

`PreferencesStore`, `LocalModelSelection` und `HealthHistoryStore` nutzen lokale JSON-Dateien. Berichtsexporte werden über eigene begrenzende Exportregeln erstellt. Testprofile sind getrennt vom normalen Benutzerprofil. Es gibt keinen belegten SQL-/SQLite-/Cloud-Datenspeicher.

Die private Ausgabe wird self-contained für `win-x64` veröffentlicht. Inno Setup integriert Desktop, Worker, eigene KI, Modell und Lizenztexte. SHA-256-Manifeste dienen der Dateiintegrität; sie ersetzen keine vertrauenswürdige digitale Signatur.

## Bewusste Grenzen

`ProductReleasePolicy.CloudAiEnabled` ist `false`; `BetaSecurityPolicy.AllowUnauthenticatedWeb` ist `false`; `RepairActions.SystemChangesEnabledInThisBuild` ist `false`. Vorhandener Code für Cloud, WebView2 oder WinGet ist deshalb nicht gleichbedeutend mit einer freigegebenen Produktfunktion.
