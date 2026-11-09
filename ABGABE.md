# Abgabe — IIoT Teil Egger: Projektabgabe (Link zum Fork)

Sakai-Seite: **In progress**. Statusfeld: **Not Started**.

Quellen:

- Sakai-Aufgabe plus Abschnitt [Abgabe](https://jhumci.github.io/MECH-M-3-IIoT/#abgabe) auf der Kurs-Website
- Mail von Christoph Egger, notiert am 09.11.2026. Die Aufgabenbeschreibung ist überarbeitet, neu ist der Abschnitt „Abgabe“.

## Frist

| | |
|---|---|
| Sakai „Due“ / „Accept Resubmission Until“ (frühere Notiz) | **27.11.2026, 12:59** |
| Aufgabentext, Kurs-Website und Mail vom 09.11.2026 | **Freitag, 27.11.2026, 23:59 Uhr** |

Die Mail nennt 23:59 Uhr. Sakai zeigte zuvor 12:59. Maßgeblich für die Bewertung ist der letzte Commit auf `main` vor der Frist. Wiederabgabe ist unbegrenzt erlaubt, ebenfalls bis zur Frist. Notenskala in Sakai: No Grade.

Abgegeben wird pro Gruppe der Link zum Fork in der Sakai-Aufgabe. Dazu gehören der Code im Fork, das README und der Link zur Bildschirmaufnahme.

Pro Gruppe genügt die Abgabe durch eine Person.

## Verbindlich ab der Mail vom 09.11.2026

- **HTTP `/status`:** Das Schema steht in `docs/iot-specs/openapi.yaml` des Original-Repositories, Version **1.2.0**. Zusätzliche Felder sind erlaubt. Im Fork ist `openapi.yaml` noch Version 1.1.0.
- **MQTT-Status:** Auch die Last-Will-Nachricht ist JSON, also `{"status": "offline"}`, kein reiner Text. Firmware prüfen. `docs/iot-specs/conventions.md` im Fork sagt noch `Last Will = offline`, und die Docstrings in `src/raspi_firmware/code.py` beschreiben eine einfache Statuszeichenkette.
- Abweichende Nachrichten anderer Gruppen abfangen, statt abzustürzen.
- „Sync fork“ auf GitHub holt die Änderungen in den Fork. Das ist nicht zwingend; Website und Spezifikationen im Original-Repository genügen. Bei Konflikten in `code.py` oder `settings.toml` die eigene Version behalten.

## Was ins Sakai-Textfeld kommt

- MQTT-Gruppenname: `iiot/group/...` *(noch eintragen)*
- Link zum Fork: https://github.com/HannahResch/MECH-M-3-IIoT-HvW-Resch

Der Fork muss öffentlich sein oder `Robo-Chris` Zugriff haben.

## Voraussetzung für die Bewertung

Alle drei Teile müssen vorliegen. Die genauen Anforderungen stehen im Abschnitt „Abgabe“ auf der Kurs-Website.

### 1. Code im Fork

- Firmware unter `src/`, lauffähig mit einer `settings.toml` nach Anleitung
- Testfälle für die HTTP-API unter `tests/`
- Containerlösung mit `docker-compose.yml` (Pfad im README), Start mit `docker compose up` nach einem frischen `git clone` und den im README beschriebenen Schritten
- Keine echten Passwörter im Repository, auch nicht in der Git-Historie: `settings.toml` mit Platzhaltern, Container-Passwörter in einer `.env` (in `.gitignore`), dazu eine `.env.example`

### 2. README.md im Hauptverzeichnis

Das README ersetzt das vorhandene README des Forks. Eine neue Person muss das System allein damit in Betrieb nehmen können. Details dürfen in andere Dateien (z. B. `docs/Dokumentation.qmd`), solange das README darauf verlinkt.

- Gruppe: Namen, MQTT-Gruppenname (`iiot/group/...`)
- Video: Link zur Bildschirmaufnahme
- Erreichter Stand: beanspruchte Bewertungsstufe aus Termin 3 und Teststufe aus Termin 2, plus was nicht funktioniert
- Überblick: Architektur (Sensor, Broker, Speicher, Dashboard), Struktur des Repositories
- Mikrocontroller einrichten: Hardware und Verkabelung, Firmware aufspielen, `settings.toml` ausfüllen, WLAN, Funktionsprüfung
- Container starten: Voraussetzungen und alle Befehle vom `git clone` bis zum laufenden System, inklusive `.env`
- Dashboard nutzen: URL, Login, was die Ansichten zeigen
- HTTP-API: Endpunkte mit `curl`-Beispiel, Ausführen der Testfälle
- Hinweise für die IT-Abteilung: ausgehende und eingehende Verbindungen für die Whitelist, Diskussion des Fernzugriffs auf die HTTP-API (Termin 2)
- Sicherheit: kurzer Absatz, was eine Produktivversion zusätzlich bräuchte

### 3. Bildschirmaufnahme (3–5 Minuten)

Laufendes System mit echtem Sensor und Live-Daten, mit Ton oder Einblendungen. Schnitte sind erlaubt. Nur zeigen, was die Lösung umfasst, in dieser Reihenfolge:

1. Gerät: Pico W mit Sensor startet, serielle Konsole zeigt WLAN und IP-Adresse.
2. MQTT: Messwerte und Status im MQTT Explorer auf dem richtigen Topic. Nach Trennung erscheint `{"status": "offline"}`.
3. HTTP-API: `GET /status`, `GET /config`, `POST /config` mit neuem Intervall. Das neue Intervall ist in den Nachrichten sichtbar. Danach laufen die Testfälle.
4. Start: `docker compose up` aus dem Repository, `docker compose ps` zeigt die laufenden Container.
5. Dashboard: Live-Daten laufen ein, Aktualisierung sichtbar.
6. Bewertungsstufen: Blick in die Datenbank (befriedigend). Ein neuer Sensor erscheint ohne Konfiguration, z. B. eine andere Gruppe oder eine Testnachricht mit `mosquitto_pub` auf `iiot/group/test-<...>/sensor/temperature/state` (gut). Geräteübersicht mit Anzahl, letzter Verbindung und Status (sehr gut). Kennzahlen (Bonus).

Das Video muss ohne Anmeldung per Link abrufbar sein (z. B. nicht gelistet auf YouTube oder eine Freigabe über OneDrive) und bis zur Notenvergabe online bleiben. Nicht ins Repository legen (GitHub lehnt Dateien über 100 MB ab). In der Aufnahme dürfen keine Passwörter zu sehen sein. Der Link steht im README.
