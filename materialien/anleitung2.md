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
[https://api.flutter.dev/flutter/widgets/Column-class.html](Column) Widget mit folgenden Widgets ergänzt (entsprechend des Screendesigns oben):

1. Text-Widget, das eine einfache Rechenaufgabe darstellt, bestehend aus zwei zufälligen Zahlen, die addiert werden sollen.
2. Textfeld-Widget, in das der Benutzer seine Lösung eingeben kann.
3. Button-Widget, um die Lösung zu überprüfen.
4. Text-Widget, das die Rückmeldung an den Benutzer gibt, ob die Lösung richtig oder falsch ist.

Die Oberfläche besteht aus einem Column-Widget, das verschiedene Widgets wie Text, TextField, ElevatedButton und Row-Widgets erwartet. Wir legen zunächst die Struktur innerhalb des Containers fest. Die Oberfläche besteht aus einem Column-Widget, das verschiedene Widgets wie Text, TextField, ElevatedButton und Row-Widgets als Chilrden aufnehmen wird.

In Flutter bezieht sich "child" auf ein einzelnes Widget, das in einem anderen Widget platziert wird, während "children" sich auf eine Liste von Widgets bezieht, die in einem Container-Widget platziert werden.

Sehen wir uns dazu die Struktur innerhalb von body an:

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
In einem nächsten Schritt werden die vier Widget-children ergänzt:

**Rechenaufgabe (Text Widget)**
Die Rechenaufgabe wird mit dem Text Widget dargestellt, dem zwei Variablen aus dem Model "MyAppState" abgerufen werden. Die Darstellung zwischen den beiden Variablen Zahl1 und Zahl2 **' + '** ist eine Verkettung der Variablen mit dem String **+** für die Darstellung der Addition. Vorsicht: Hier wird nicht addiert, sondern nur dargestellt. Die eigentliche Addition wird im MyAppState Widget stattfinden.

```dart
Text(Zahl1' + 'Zahl2+' =')
 ```
**Lösungseingabe und Prüfung der Lödung (Textfeld und Button Widget)**
Das nächsten beiden Widgets in den Children werden in einer **Row**, also Zeile dargestellt. Damit kann das Texteingabefeld und der Button nebeneinander dargestellt werden.
```dart
 Row(
              children: [
                
                //Textfeld Eingabe
                Expanded(
                  child: TextField(
                    controller: appState.eingabe,
                    decoration: InputDecoration(
                      border: UnderlineInputBorder(),
                      hintText: 'Lösung',
                    ),
                  ),
                ),

                //Antwortbutton
                ElevatedButton(
                  onPressed: () {
                    appState.check();
                  },
                  child: Text('prüfen'),
                ),
              ],
            ),
```
Das Textfeld wird mit einem TextEditingController namens "eingabe" verknüpft (den wir später im MyAppState definieren) und der es ermöglicht, den Inhalt des Textfelds zu lesen und zu ändern. Der Button wird durch ein ElevatedButton-Widget dargestellt und durch eine onPress-Funktion ausgelöst, die die Funktion "check" ausführt, die ebenfalls später in einem anderen Teil des Codes definiert ist.

**Test für Rückmeldung ob richtig oder falsch (Text Widget)**
 Der Text wird durch die Variable "feedback" dargestellt und kann den Text "richtig" oder "falsch" enthalten.

```dart
Text(
  appState.feedback,
  style: TextStyle(fontSize: 50, color: Colors.black),
  )
```

Die gesamte App sieht nun folgendermaßen aus. Nun fehlt noch das Model in **MyAppState**
```dart
import 'dart:math';

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

    notifyListeners();
  }
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
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            //Rechenaufgabe (verkettete Strings)
            Text(
              appState.number1.toString() +
                  ' + ' +
                  appState.number2.toString() +
                  ' =',
              style: TextStyle(fontSize: 60),
            ),

            //Lösungseingabe (Textfeld + Button in einer Row)
            Row(
              mainAxisAlignment:
                  MainAxisAlignment.spaceEvenly, //verteile auf Bildschirmbreite
              children: [
                //Textfeld Eingabe
                Expanded(
                  child: TextField(
                    controller: appState.eingabe,
                    decoration: InputDecoration(
                      border: UnderlineInputBorder(),
                      hintText: 'Lösung',
                    ),
                  ),
                ),

                //Antwortbutton
                ElevatedButton(
                  onPressed: () {
                    appState.check();
                  },
                  child: Text('prüfen'),
                ),
              ],
            ),

            //weitere Row für Rückmeldung ob richtig oder falsch
            Row(
              mainAxisAlignment:
                  MainAxisAlignment.center, //am Bildschirm zentrieren

              children: [
                Text(
                  appState.feedback,
                  style: TextStyle(fontSize: 50, color: Colors.black),
                ), //Rückgabetext
              ],
            )
          ],
        ),
      ),
    );
  }
}
```

## Model: MyAppState
Bevor wir das Model in MyAppState implementieren, einige Vorüberlegungen, was benötigt wird.
1. Zunächst werden die beiden Zufallszahlen ermittelt.
2. Dann muss die Benutzereingabe der Lösung gespeichert werden.
3. Zudem muss geprüft werden, ob die Benutzereingabe mit der Summe der beiden Zufallszahlen übereinstimmt.
4. Je nachdem, ob diese richtig oder falsch ist, wird die Rückgabe in einer Variable mit "richtig" oder "falsch" festgelegt.

Damit die Kommunikation zwischen Screendesign in **MyHomePage** und dem Model in **MyAppState** funktioniert, wird über den **ChangeNotifier** geregelt.

Dieser wird im Screendesign von **MyHomePage** über das Drücken des Buttons ausgelöst, wo eine Methode **check** aufgerufen wird. 

```dart
onPressed: () {
     appState.check();
              },
```
**appState** wird im Programm in **MyHomepage** über
```dart
 var appState = context.watch<MyAppState>();
```
definiert.

**Kleiner Exkurs dazu** 
> **watch** ist eine Methode, die in Verbindung mit dem **Provider**-Paket verwendet wird, um die Aktualisierung von Widgets basierend auf Änderungen an den Daten im Provider-Objekt zu ermöglichen. Der Flutter-Code var appState = context.watch<MyAppState>(); verwendet watch, um das MyAppState-Objekt aus dem Provider zu erhalten und es der Variablen appState zuzuweisen. Dies bedeutet, dass die Variable appState nun auf die Eigenschaften und Methoden von MyAppState zugreifen und diese verwenden kann. Wenn sich eine Änderung in MyAppState ergibt, wird appState aktualisiert und das Widget, das auf appState hört, wird automatisch neu gerendert, um die neuen Daten anzuzeigen.

Die Methode **check** wird dann folgendermaßen im Widget **MyAppState** beschrieben:
  
```dart
  void check(){
    var summe_eingabe = int.parse(eingabe.text); //Typenumwandlung von String aus Textfeld nach Integer
    var summe_aufgabe = number1 + number2;
    if(summe_eingabe == summe_aufgabe) {
      feedback = "richtig";
    } else {
      feedback = "falsch";
    }
    notifyListeners();
  }
}
```
  
Der obige Flutter-Code definiert eine Methode *check()*, die eine Eingabe vom Benutzer auf Richtigkeit prüft und eine Rückmeldung in Form von feedback zurückgibt. Die Methode führt folgende Schritte aus:

1. Holt den Inhalt des Textfelds eingabe und wandelt ihn in einen Integer mit int.parse() um. Der Integer wird in summe_eingabe gespeichert.
2. Berechnet die Summe summe_aufgabe aus den beiden Zufallszahlen number1 und number2.
3. Vergleicht die eingegebene Summe summe_eingabe mit der berechneten Summe summe_aufgabe.
4. Wenn die beiden Summen übereinstimmen, setzt die Methode feedback auf "richtig", andernfalls auf "falsch".
  
Die Methode notifyListeners() wird aufgerufen, um alle Widgets zu benachrichtigen, die auf Änderungen im MyAppState-Objekt hören. Dadurch wird eine Aktualisierung der Benutzeroberfläche ausgelöst, um das Ergebnis der Überprüfung anzuzeigen.
  
Nun fehlen noch die Variablen und Zufallsvariablen, die ebenfalls in **MyAppState** im Model definiert werden:
```dart
  var number1 = Random().nextInt(90); //Zufalls-Summand 1
  var number2 = Random().nextInt(90); //Zufalls-Summand 2
  String feedback = '';

  TextEditingController eingabe = TextEditingController();
```
1. **number1**: Eine Zufallszahl zwischen 0 und 89, die als erster Summand in der Rechenaufgabe verwendet wird.
2. **number2**: Eine weitere Zufallszahl zwischen 0 und 89, die als zweiter Summand in der Rechenaufgabe verwendet wird.
3. **feedback**: Eine Zeichenkette, die zur Rückmeldung verwendet wird, ob die vom Benutzer eingegebene Summe korrekt ist oder nicht. Wenn die Eingabe korrekt ist, wird feedback auf "richtig" gesetzt, andernfalls auf "falsch".
4. **eingabe**: Ein TextEditingController-Objekt, das zum Speichern der vom Benutzer eingegebenen Summe verwendet wird. Dieses Objekt wird in einem Textfeld im Benutzerinterface verwendet, um die Eingabe zu ermöglichen.
  
## Gesamte App
Die gesamte App finden Sie hier:  https://github.com/bernhardstandl/simple_first_app/blob/master/lib/main.dart oder direkt über die Aufgabe von GitHub Classroom: https://classroom.github.com/a/ftpm1rgQ
 
