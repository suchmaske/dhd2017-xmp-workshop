# Tutorial exiftoolGUI
*Oliver Pohl, Torsten Schrade*

## Allgemeines

* Free Open Source Software

* exiftoolGUI (Windows only)
  - Download: http://u88.n24.queensu.ca/~bogdan/exiftoolgui516.zip
* pyExiftoolGUI (plattformunabhängig)
  - Download: https://hvdwolf.github.io/pyExifToolGUI/
  - Unstable

## exiftoolGUI

### Vorbereitung
* exiftool installieren
* exiftool-Konfiguration muss im PATH angegeben sein
* exiftool-Konfiguration kann sonst *nicht* von exiftoolGUI benutzt werden
* Mit Terminal/CMD kopieren
  ```
  $ cp conf/cvma.ExifTool_config C:\Windows
  ```
* Der Windows-Explorer erwartet einen Dateinamen vor dem Punkt. Daher muss mit dem Terminal umbenannt werden.

### exiftoolGUI Benutzung

* Rechte Spalte > XMP
  - Zeigt alle XMP Daten an
  ![exiftoolGUI: XMP-Daten anzeigen](img/exiftoolGUI/exiftoolGUI_xmp_view.png)

* Workspace: Metadaten bearbeiten
  - Aus den anderen Reitern ein Feld auswählen -> Rechtsklick -> "Add tag to workspace"
  - Beispiel: Workshop
  ![exiftoolGUI: Add to Workspace](img/exiftoolGUI/exiftoolGUI_add_to_workspace.png)

  - Im Workspace-Reiter unten einen neuen Wert eingeben
    + Eingabe mit Enter bestätigen
    + Save-Button klicken
  ![exiftoolGUI: Wert bearbeiten](img/exiftoolGUI/exiftoolGUI_edit_value.png)
  ![exiftoolGUI: Wert bearbeitet, noch nicht gespeichert](img/exiftoolGUI/exiftoolGUI_value_edited_not_saved.png)

  - Wenn Konfiguration nicht in ```C:\Windows``` hinterlegt wurde, gibt es eine Fehlermeldung
  ![exiftoolGUI: Fehler](img/exiftoolGUI/exiftoolGUI_config_error.png)

  - Wenn Konfiguration richtig ist und geladen wurde kommt keine Fehlermeldung:
  ![exiftoolGUI: Wert bearbeitet, und gespeichert](img/exiftoolGUI/exiftoolGUI_value_edited_and_saved.png)

* Workspace anpassen

  - Program > Workspace Manager
  ![exiftoolGUI: Workspace Manager](img/exiftoolGUI/exiftoolGUI_workspace_manager.png)

  - XMP-Felder und Labels bearbeiten
  ![exiftoolGUI: Workspace Manager anpassen](img/exiftoolGUI/exiftoolGUI_workspace_manager_change.png)

  - Label wird in der Bearbeitungsansicht geändert
  ![exiftoolGUI: Label geändert](img/exiftoolGUI/exiftoolGUI_workspace_label_changed.png)

## Tests

### exiftool

* Eingegebenen Werte mit exiftool überprüfen

```
$ exiftool -config conf/cvma.ExifTool_config -xmp-cvma:Workshop img/csm_Adolfseck_Hl_Familie.jpg
```
> Workshop                        : DHd 2017 with exiftoolGUI

### Fotostation

* Metadaten mit Fotostation betrachten

![exiftoolGUI: Eingabe mit Fotostation überprüfen](img/fotostation/Fotostation_Metadata_check_exiftoolGUI.png)
