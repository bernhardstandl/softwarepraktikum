# Softwarepraktikum
Informationen und Unterlagen zum Softwarepraktikum


## Semesterplan

| Datum  | Thema | Unterlagen |
| ------------- | ------------- | ------------- |
| 18.4.  | Vorbesprechung, Inhalte, Setup | [Foliensatz](sp_foliensatz.pdf) |
| 25.4.  | Gemeinsame Entwicklung der ersten Flutter App,  Entwicklung von Projektideen |  |


## Installation von Flutter
* Laden und installieren Sie Visual Studio Code https://code.visualstudio.com/download
* Installieren Sie die Flutter SDK (Software Development Kit ) https://docs.flutter.dev/get-started/install und folgen Sie genau der Anleitung für das jeweilige Betriebssystem

# Tutorial 1
*
*

# Tutorial 2
* Öffnen Sie das Tutorial: https://codelabs.developers.google.com/codelabs/flutter-codelab-first#2
* Erstellen Sie das erste Flutter Projekt, so wie im Tutorial beschrieben
* Nehmen Sie die Änderungen in pubspec.yaml vor. An welcher Stelle müssen Ergänzungen vorgenommen werden? Tipp: https://pub.dev/
* Nehmen Sie die Änderungen in analysis_options.yaml vor. Wozu werden diese Einstellungen benötigt? Was sind Lints? Welche werden im Tutorial vorgeschlagen? https://dart-lang.github.io/linter/lints/index.html
* Kopieren sie den Code von main.dart im Tutorial in VS Code
* 

![Alt text](https://g.gravizo.com/source/custom_mark10?https%3A%2F%2Fraw.githubusercontent.com%2FTLmaK0%2Fgravizo%2Fmaster%2FREADME.md)
<details> 
<summary></summary>
custom_mark10
  digraph G {
    size ="4,4"
    main [shape=box]
    main -> parse [weight=8]
    parse -> execute
    main -> init [style=dotted]
    main -> cleanup
    execute -> { make_string; printf}
    init -> make_string
    edge [color=red]
    main -> printf [style=bold,label="100 times"]
    make_string [label="make a string"]
    node [shape=box,style=filled,color=".7 .3 1.0"]
    execute -> compare
  }
custom_mark10
</details>
