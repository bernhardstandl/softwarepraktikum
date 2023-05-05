# Anleitung zu der einfachen Rechenapp


## Vorgaben
Die einfache Rechenapp soll folgendermaßen konstruiert sein:

**Funktion** 
* Es wird eine Aufgabe einer Addition zweier Zufallszahlen kleiner als 100 dargestellt.
* Nutzer der App geben die Lösung in einem Textfeld ein und prüfen über einen Button die Eingabe. 
* Wenn die Lösung falsch eingegeben wurde, wird dies in einem Textlabel mit "falsch" rückgemeldet, wenn die Lösung richtig eingegben wurde, word "richtig" rückgemeldet.

**Design** eine Seite:

<img src="pic/design.png " width="20%">

## Vorbereitung
Also Grundlage verwenden wir das Grundgerüst aus der Tutorial App mit Changenotifier. Hier der Code, eine Beschreibung dazu ist unterhalb.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';


void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => MyAppState(),
      child: MaterialApp(
        title: 'Rechenübungen',
        theme: ThemeData(
          useMaterial3: true,
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.green),
        ),
        home: MyHomePage(),
      ),
    );
  }
}

class MyAppState extends ChangeNotifier {
    // Model
    notifyListeners();
}

class MyHomePage extends StatelessWidget {
  @override

  Widget build(BuildContext context) {
    var appState = context.watch<MyAppState>();
    

    return Scaffold(

        //Titelleiste
        appBar: AppBar(
          centerTitle: true,
          title: Text("Übung zur Addition"),
          backgroundColor: Colors.green,
        ),
              
        body: Container(

        ),
    );
  }
}

```
Zunächst werden die benötigten Pakete importiert, darunter das [Material](https://docs.flutter.dev/ui/material) Paket und das [Provider](https://medium.com/bancolombia-tech/flutter-provider-what-is-it-what-is-it-for-and-how-to-use-it-47d6941860d7) Paket.

In der main-Methode wird die App gestartet und das MyApp-Widget ausgeführt.

Das MyApp-Widget ist ein [StatelessWidget](https://api.flutter.dev/flutter/widgets/StatelessWidget-class.html), das ein [ChangeNotifierProvider-Widget](https://flutterbyexample.com/lesson/change-notifier-provider) enthält. Hier wird der Provider verwendet, um den Zustand der App zu verwalten, indem er das MyAppState-Widget als Model in einem ChangeNotifierProvider erstellt.

Das MyAppState-Widget ist ein ChangeNotifier, das das Model der App repräsentiert. Das Model einer App ist sozuagen die "Logik" der App. Hier ist derzeit keine Funktionalität implementiert, aber das notifyListeners()-Methode wird aufgerufen, um Änderungen an den Listeners zu signalisieren, die Änderungen an die App zurückzugeben. Später werden wir hier die Zufallszahlen für die Addition erstellen und prüfen, ob die Nutzereingabe richtig war.

Das MyHomePage-Widget ist ebenfalls ein StatelessWidget, das auf das MyAppState-Widget zugreift, indem es die watch()-Methode des Provider-Pakets verwendet. Hier wird das UI der App innerhalb des [Scaffold](https://www.flutter.de/artikel/was-du-%C3%BCber-das-flutter-scaffold-widget-wissen-solltest) Widgets erstellt. Es gibt eine Titelleiste, die ein grünes Farbschema hat und den Titel "Übung zur Addition" trägt. Der Inhalt des Body ist derzeit noch leer, später wird hier die Darstellung der Addition und Textfeld für die Eingabe des Ergebnisses Addition und ein Button hinzugefügt.



## Screendesign
In einem nächsten Schritt wird das Screendesign im Widget MyHomePage erstelt. Dazu wird das vorhandene
[https://api.flutter.dev/flutter/widgets/Column-class.html](Column) Widget ergänzt (entsprechend des Screendesigns oben):

1. Text-Widget, das eine einfache Rechenaufgabe darstellt, bestehend aus zwei zufälligen Zahlen, die addiert werden sollen.
2. Textfeld-Widget, in das der Benutzer seine Lösung eingeben kann.
3. Button-Widget, um die Lösung zu überprüfen.
4. Text-Widget, das die Rückmeldung an den Benutzer gibt, ob die Lösung richtig oder falsch ist.

Die Oberfläche besteht aus einem Column-Widget, das verschiedene Widgets wie Text, TextField, ElevatedButton und Row-Widgets erwartet. Wir legen zunächst die Struktur innerhalb des Containers fest. Die Oberfläche besteht aus einem Column-Widget, das verschiedene Widgets wie Text, TextField, ElevatedButton und Row-Widgets als Chilrden aufnehmen wird.

In Flutter bezieht sich "child" auf ein einzelnes Widget, das in einem anderen Widget platziert wird, während "children" sich auf eine Liste von Widgets bezieht, die in einem Container-Widget platziert werden.


```dart
body: Container(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            crossAxisAlignment: CrossAxisAlignment.center,
            
            
            children: [
                 //Rechenaufgabe (Text Widget)

                 //Lösungseingabe (Textfeld Widget)        

                 //Prüfung der Lösung (Button Widget)      
                
                //Test für Rückmeldung ob richtig oder falsch (Text Widget)
            ],
       );
 ```
