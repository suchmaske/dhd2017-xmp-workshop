# Tutorial Exiftool
*Oliver Pohl, Torsten Schrade*

## Installation

### Download (Windows + MacOS)
* Download: http://www.sno.phy.queensu.ca/~phil/exiftool/
* Anleitung: http://www.sno.phy.queensu.ca/~phil/exiftool/install.html

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
        + => ```-xmp-dc:title```

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

    - Allgemein
    ```
    $ exiftool -config [config-file] [befehl]
    ```
    > Stellt sicher, dass Felder aus eigenen Vokabularen und Standards gelesen werden können

    - Beispiel
    ```
    $ exiftool -config conf/cvma.Exiftool_config img/csm_Adolfseck_Hl_Familie.jpg
    ```
    > Felder aus dem CVMA-eigenen Standard werden nun gelesen


* Feld aus dem eigenen Standard auslesen

    - Gleiches Prinzip wie beim Auslesen anderer Felder: ```-xmp-[ns]:[feld]```

    - Beispiel
    ```
    $ exiftool -config conf/cvma.Exiftool_config -xmp-cvma:IconclassDescription img/csm_Adolfseck_Hl_Familie.jpg
    ```

* Konfiguration anschauen

    - Perl-Datei (exiftool ist eine Perl-Library)

    ```
    %Image::ExifTool::UserDefined::cvma = (
        GROUPS => { 0 => 'XMP', 1 => 'XMP-cvma', 2 => 'Image' },
        NAMESPACE => { 'cvma' => 'https://lod.academy/cvma/ns/xmp/' },

        ...
        IconclassDescription => { },
        ...
        )
    ```
    > CVMA-Namensraum und dazugehörige Felder werden definiert.

    - Konfiguration wird zum Auslesen und Manipulieren benötigt!

### Daten eingeben

* Generelle Syntax

    - Allgemein: ```-xmp-[ns]:[feld]=[wert] [datei]```
        + ns (Namensraum), zB. dc (Dublin Core)
        + feld (Feld im Namensraum), title
        + => ```-xmp-dc:title=Kirchenfenster```

    - Beispiel (ohne Config)
    ```
    $ exiftool -xmp-dc:title=Kirchenfenster img/csm_Adolfseck_Hl_Familie.jpg
    ```

    - Beispiel (mit Config)
    ```
    $ exiftool -config conf/cvma.ExifTool_config -xmp-cvma:Column=b img/csm_Adolfseck_Hl_Familie.jpg
    ```

* Mehrere Felder

    - Allgemein:
    ```
    $ exiftool -xmp-[ns]:[feld_1]=[wert] ... -xmp-[ns]:[feld_n]=[wert] [datei]
    ```

    - Beispiel:
    ```
    $ exiftool -xmp-dc:title=Kirchenfenster -xmp-dc:creator=Me img/csm_Adolfseck_Hl_Familie.jpg
    ```

* Bags (Listen)

    > Mehrere Einträge im selben Feld

    - In der Konfigurationsdatei muss das Feld als Bag deklariert sein
    ```
    IconclassNotation => { List => 'Bag' },
    ```

    - Dasselbe Feld mehrmals beschreiben

        + Allgemein
        ```
        $ exiftool -config [config] -xmp-[ns]:[feld_x]=[wert_1] -xmp-[ns]:[feld_x]=[wert_2] [datei]
        ```

        + Beispiel
        ```
        $ exiftool -config conf/cvma.ExifTool_config -xmp-cvma:IconclassNotation=73A22 -xmp-cvma:IconclassNotation=SomethingDifferent img/csm_Adolfseck_Hl_Familie.jpg
        ```

* (Struct)
