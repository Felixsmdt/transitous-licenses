# Lizenz bei Träwelling aktivieren

Träwelling zeigt für Verbindungen die Lizenz der verwendeten Fahrplandaten an. Wenn für eine Verbindung keine Lizenz hinterlegt ist, wird sie gar nicht angezeigt. Diese Anleitung zeigt, wie du eine Lizenz eintragen und einen Pull Request (PR) über die GitHub-Weboberfläche stellen kannst, ganz ohne Kommandozeile.

## Schritt 1: Den richtigen Dateinamen herausfinden

Öffne https://traewelling.de/debug/motis-sources und suche die Quelle, für die du eine Lizenz hinzufügen möchtest. Merke dir den genauen Dateinamen (z. B. `de_DELFI.gtfs.zip`).

## Schritt 2: Die Datei `licenses.json` auf GitHub öffnen

Navigiere im Repository zu [`licenses.json`](../licenses.json) und klicke oben rechts auf das Stift-Symbol ("Edit this file").

## Schritt 3: Lizenz eintragen

Es gibt zwei Fälle:

### Fall A: Bekannte Open-Source-Lizenz (z. B. CC-BY-4.0, ODbL-1.0)

Füge im Abschnitt `"sources"` einen neuen Eintrag hinzu:

```json
{
  "file": "xx_Meine-Quelle.gtfs.zip",
  "spdx": "CC-BY-4.0",
  "url": "https://link-zur-datenquelle.example",
  "custom_license": null
}
```

Den richtigen SPDX-Bezeichner findest du unter https://spdx.org/licenses/.

### Fall B: Eigene oder proprietäre Lizenz

Zuerst im Abschnitt `"proprietary_licenses"` einen neuen Eintrag hinzufügen:

```json
{
  "identifier": "Mein Verkehrsbetrieb Lizenz",
  "name": "Mein Verkehrsbetrieb Open Data Lizenz",
  "attribution_text": null,
  "url": "https://link-zur-lizenzbeschreibung.example"
}
```

Dann im Abschnitt `"sources"` darauf verweisen:

```json
{
  "file": "xx_Meine-Quelle.gtfs.zip",
  "spdx": null,
  "url": "https://link-zur-datenquelle.example",
  "custom_license": "Mein Verkehrsbetrieb Lizenz"
}
```

Der Wert bei `"custom_license"` muss exakt dem `"identifier"` aus `proprietary_licenses` entsprechen.

### Welche Lizenzen sind erlaubt?

Eine Lizenz muss folgende Bedingungen erfüllen:

- Nutzung, Weitergabe und Bearbeitung der Daten muss erlaubt sein
- Keine Lizenzgebühren oder Nutzungsentgelte
- Nicht produkt- oder technologiespezifisch
- Einschränkungen sind erlaubt, müssen aber klar angegeben sein (z. B. nur nichtkommerzielle Nutzung)

## Schritt 4: Pull Request erstellen

1. Scrolle auf der Bearbeitungsseite nach unten zu "Commit changes"
2. Wähle "Create a new branch for this commit and start a pull request"
3. Gib dem Branch einen kurzen Namen (z. B. `add-license-for-DELFI`)
4. Klicke auf "Propose changes"
5. Auf der nächsten Seite füllst du die PR-Vorlage aus:
   - **Country / Land**: z. B. Deutschland
   - **License / Lizenz**: Name der Lizenz
   - **Source / Quelle**: Dateiname aus Schritt 1
   - **Notes / Anmerkungen**: Alles, was noch wichtig ist
6. Klicke auf "Create pull request"

Fertig! Der PR wird dann geprüft und bei Freigabe zusammengeführt.
