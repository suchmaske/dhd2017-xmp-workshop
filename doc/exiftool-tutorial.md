# Tutorial Exiftool 
*Oliver Pohl, Torsten Schrade*

## Installation

### Download (Windows + MacOS)
Download: http://www.sno.phy.queensu.ca/~phil/exiftool/
Anleitung: http://www.sno.phy.queensu.ca/~phil/exiftool/install.html

### Windows
* ```exiftool(-k).exe``` zu ```exiftool.exe``` umbennen und nach ```C:\Windows``` verschieben.
* exiftool kann nun von CMD überall aufgerufen werden

### Ubuntu

```
$ sudo apt-get install libimage-exiftool-perl perl-doc 
```

### Test
In der Kommandozeile / CMD
```
$ exiftool -ver
```
Output sollte eine Versionsnummer sein wie "10.41" oder "10.10".

### Daten auslesen

* Generelle Syntax: exiftool + Datei
```
$ exiftool [datei]
```

* Konkretes Beispiel
```
$ exiftool img/csm_Adolfseck_Hl_Familie.jpg
```
> Gibt Liste aus

* XMP-Daten auslesen

```
$ exiftool -X img/csm_Adolfseck_Hl_Familie.jpg 
```
> Gibt RDF/XML aus

* Feld auslesen

    - Allgemein
    ```
    $ exiftool [feldname] [datei]
    ```
    
    - Generell: ```-xmp-[ns]:[feld]```
        + ns (Namensraum), zB. dc (Dublin Core)
        + feld (Feld im Namensraum), title
        + => -xmp-dc:title
    
    - Beispiel
    ```
    $ exiftool -xmp-dc:creator img/csm_Adolfseck_Hl_Familie.jpg 
    ```

* Mehrere Felder auslesen

    - Allgemein
    ```
    $ exitool [feld1] [feld2] ... [feldn] [datei]
    ```
    
    - Beispiel
    ```
    $ exiftool -xmp-dc:creator -xmp-dc:title img/csm_Adolfseck_Hl_Familie.jpg
    ```
    
    > Gibt ein Feld pro Zeile aus

* Gegenprobe: Feld aus eigenem Standard versuchen auszulesen

    - Gleiches Prinzip: ```-xmp-[ns]:[feld]```
        + ns: cvma
        + feld: IconclassDescription
    - Beispiel
    ```
    $ exiftool -xmp-cvma:IconclassDescription img/csm_Adolfseck_Hl_Familie.jpg
    ```
    > Befehl funktioniert nicht, weil der Namensraum unbekannt ist

### Konfiguration laden

* Syntax
* Feld aus dem eigenen Standard auslesen
* Konfiguration anschauen

### Daten eingeben

* Generelle Syntax
* Ein Feld
* Mehrere Felder
* (Bags)
* (Struct)


