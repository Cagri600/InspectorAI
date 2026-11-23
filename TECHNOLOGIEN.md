# Nachgewiesenes Technologieinventar

Analysierter Bestand: 512 Dateien des aktuellen Quellbaums. Die Zahlen beschreiben Dateien, keine Codequalität oder persönlichen Arbeitsstunden.

## Sprachen und Formate

| Sprache/Format | Dateien | Verwendung |
|---|---:|---|
| C# | 153 | Desktop, Diagnostikbibliothek, Worker und native Testprogramme |
| Python | 114 | Statische Vertrags-/Quellprüfungen und Paketierungs-/Archivwerkzeuge; keine Laufzeitvoraussetzung der fertigen App |
| PowerShell | 65 | Build-, Prüf-, Installations- und Verteilungsautomatisierung; teils historische Skripte |
| Windows CMD/Batch | 14 | Start-/Build-Einstiegsskripte |
| Inno Setup/Pascal Script | 1 `.iss` | Setupdefinition, Initialisierung der gebündelten KI, Uninstaller-Hooks |
| MSBuild/XML/NuGet-Metadaten | 7 `.csproj`, 1 `.props`, 1 `.nuspec` | Zielplattformen, Referenzen, Versionierung und Buildregeln |
| YAML | 1 | Vorhandener GitHub-Actions-Workflow; aktuell nicht als erfolgreich gelaufen belegt |
| JSON | 7 im Quellbaum | Bundle-/Statusmetadaten; zusätzlich Laufzeitverträge, Einstellungen und Berichte im C#-Code |
| Markdown/Text/SVG/ICO | 120 `.md`, 25 `.txt`, 1 `.svg`, 1 `.ico` | Dokumentation, Lizenztexte und Assets |

Keine JavaScript-, TypeScript-, HTML-, CSS-, SQL-, Dockerfile- oder package.json-Dateien im analysierten aktuellen Quellbaum. Keine belegte React-/Angular-/Vue-/ASP.NET-/Electron-/SQLite-/Docker-Laufzeitarchitektur. Ein SVG ist ein Bildformat, kein Beleg einer Weboberfläche.

## Laufzeit und deklarierte Abhängigkeiten

| Technologie | Version/Nachweis | Rolle |
|---|---|---|
| .NET | Projekte `net10.0` / `net10.0-windows`; ausgelieferte Laufzeit 10.0.13 | C#-Laufzeit und Windows Desktop, self-contained `win-x64` |
| Windows Forms | `UseWindowsForms=true` | Native Oberfläche, Forms, Tabellen und Ereignisse |
| System.Drawing / GDI+ | .NET-Windows-Laufzeit | Eigengezeichnete Karten/Buttons und Grafikmessung |
| System.Management | NuGet 10.0.14 | WMI-Hardware-/Treiberabfragen |
| Microsoft.Web.WebView2 | NuGet 1.0.4314.35 | Referenz und gesperrter historischer Webpfad; aktuelle native Startoberfläche benötigt ihn nicht als Web-Dashboard |
| Ollama | Bundlemetadaten 0.40.16 | Mitgelieferter lokaler Modellserver; keine selbst entwickelte KI-Laufzeit |
| Qwen2.5:1.5b | Paketname aus Bundle/Initialisierung; Q4_K_M laut mitgelieferten Lizenz-/Bundlehinweisen | Mitgeliefertes Sprachmodell, CPU-Ausgabe, kein eigenes Training |
| llama.cpp/ggml, CPU-Bibliotheken, winpthreads | Lizenz-/Dateibestand des KI-Bundles | Transitive native Bestandteile von Ollama; keine zusätzlich selbst integrierten Python-ML-Frameworks |
| Inno Setup | vorhandene `InspectorAI.iss` und dokumentierter Compilerlauf | Per-user Windows-Installer |
| NuGet und MSBuild | Projektdateien | Restore/Build; SDK für Entwicklung, nicht beim Anwender nötig |

Die vollständigen Einträge der ausgelieferten Desktop-/Worker-`.deps.json` stehen in [ABHAENGIGKEITEN.csv](ABHAENGIGKEITEN.csv) und [WORKER-ABHAENGIGKEITEN.csv](WORKER-ABHAENGIGKEITEN.csv). Sie unterscheiden Projekte, NuGet-Pakete, Referenzen und Runtimepacks. Die übrigen `System.*`-/`Microsoft.Win32.*`-APIs sind überwiegend Bestandteil der .NET-Laufzeit, keine separaten Paketreferenzen.

[AUSGELIEFERTE-LAUFZEITMODULE.csv](AUSGELIEFERTE-LAUFZEITMODULE.csv) ergänzt die vollständige Liste der 491 ausgelieferten EXE-/DLL-Dateien mit relativen Pfaden, Dateiversionen und Größen. Das sind Laufzeitmodule einschließlich Frameworkdateien und transitiver nativer Varianten, nicht 491 unabhängige Frameworks oder eigene Bibliotheken.

## Tatsächlich verwendete APIs und Techniken

- `System.Text.Json`: Datenmodelle, begrenztes Parsing, JSON-Verträge/Schema, lokale Dateien und Exporte.
- `HttpClient`: lokaler Ollama-Transport, Zeitlimits und Response-Validierung. Cloud-Client im Quellbaum ist deaktiviert.
- Historischer/inaktiver Cloudpfad: `CloudAiClient.cs` nennt die OpenAI-Responses-HTTP-API (`/v1/responses`). Kein OpenAI-SDK als NuGet-Paket und keine aktive Cloudfunktion dieser privaten Ausgabe.
- `Task`, `async/await`, `CancellationToken`, `WaitAsync`, `SemaphoreSlim`: Nebenläufigkeit und Abbruch.
- `System.Diagnostics.Process`: isolierte Sammler, `nvidia-smi`, eigene KI und fester Worker-Aufruf; keine beliebigen KI-Kommandos.
- `System.Diagnostics.Eventing.Reader`: Windows-Ereignisse; `System.Management`: WMI.
- `Microsoft.Win32.Registry`, Registry32/Registry64: vorhandene Komponenten-/Softwareerkennung.
- `System.Net.NetworkInformation`, DNS-APIs, `DriveInfo` und Windows-Speicherabfragen: lokale Netzwerk-/Datenträgerdaten; optionale externe Abfragen getrennt.
- P/Invoke/Win32: unter anderem `GetSystemTimes`, `GlobalMemoryStatusEx`, Fensternachrichten und Windows-Jobobjekte.
- `Mutex`, GUID-/Run-ID-Verträge, Dateisperren, Journale und feste Aktionslisten: Prozess-/Operationsgrenzen.
- SHA-256, Kryptografie- und Updateprüfcode: Integritäts-/Sicherheitsmechanismen; keine vorhandene vertrauenswürdige Codesignierung behaupten.
- JSON-Dateien statt Datenbank; ZIP und Dateimanifeste für Verteilung/Sicherung.
- Eigene .NET-Konsolenassertions und native Testharnesses; kein nachgewiesenes xUnit/NUnit/MSTest-Paket.
- GitHub Actions ist konfiguriert (`windows-latest`, `setup-dotnet`, Checkout/Artifact-Actions), aber der Workflow referenziert historische Snapshot-/Buildpfade und ist vor Aktivierung zu überprüfen.

FFmpeg, das nur für das Präsentationsvideo verwendet wird, ist **keine InspectorAI-Technologie oder Laufzeitabhängigkeit**.
