# Nachweisbarer Teststatus

Stand der privaten Testausgabe vom 23.11.2026. Hier wurden vorhandene Nachweise ausgewertet; die Erstellung dieser Portfolio-Unterlagen ist kein neuer Testlauf der gesamten Software.

| Prüfung | Belegter Umfang | Grenze |
|---|---|---|
| Zusammenhängender Benutzerablauf | 22 bestandene native Windows-Prüfungen mit realen Sammlern, lokalem Modell, Chat, Folgefrage, Werkzeug, Abbruch, Export und Speicherung | Offscreen-Form-/Handlerprüfung, keine vollständige manuelle Abnahme aller Dialoge |
| Neues Programmfenster/Prozess | Gespeicherte Einstellungen, Modell und Verlauf erneut geladen | Kein echter Betriebssystem-Neustart |
| Experten-Freigabe | Ablehnen, erneute Anfrage und erfolgreiche Zustimmung tatsächlich geklickt; Modell antwortet mit Messbelegen | Keine Garantie jeder denkbaren Fehlersituation |
| DPI | Echte 125/175 Prozent und Rückwechsel; gezielte native Größenprüfungen; frühere 100/150-Nachweise | Physisches Misch-DPI und lückenlose visuelle Matrix offen; breiter Audit nicht pauschal grün |
| Installer-Lifecycle | Installation/Upgrade/Deinstallation auf dem vorhandenen Windows mit eigener Test-AppID und eigenem Profil; Einstellungen erhalten | QA-Variante des Skripts ohne Kompression; keine unveränderte finale EXE auf sauberem Gast installiert |
| Finale Weitergabe-EXE | Normaler deutscher Assistent tatsächlich geöffnet | Kein sauberer Windows-Gast verfügbar |
| Portable | Finales ZIP dekomprimiert, 524 Dateien gehasht, enthaltene KI initialisiert und App sichtbar gestartet | Auf demselben Host |
| Quellarchiv | 512 Dateien dekomprimiert und per SHA-256 mit der Quelle abgeglichen | Archivprüfung ist kein Funktionsbeweis |
| Reparaturen | Ausführungssperren und negative/Abbruchpfade geprüft | Keine positiven isolierten systemändernden Tests; Funktionen bleiben gesperrt |

Die zugehörigen Originalnachweise liegen lokal in der privaten Auslieferung unter `Pruefnachweise/`, insbesondere `finaler-benutzerablauf`, `Installer-Lifecycle`, `archiv-integritaet.json`, `Portable-Offline-KI.json` und `DPI-und-Freigabe/`. Sie werden wegen möglicher personenbezogener bzw. rechnerbezogener Inhalte nicht unbesehen ins öffentliche Repository kopiert.

Ein vorhandener GitHub-Actions-Workflow ist kein Beweis eines gelaufenen oder erfolgreichen GitHub-Builds. Es werden keine Betriebszuverlässigkeit, Testabdeckung in Prozent oder Nutzerzahlen erfunden.
