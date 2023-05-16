

## Struktur
Innerhalb des MaterialApp-Widgets wird ein Scaffold-Widget verwendet, um die grundlegende Struktur der App zu definieren. Das Scaffold-Widget stellt eine App-Leiste (AppBar) und einen Körper (body) bereit. Die AppBar enthält einen Titel, der mit dem Text-Widget definiert wird und den Wert "Layout einer App" hat. Der Body der App ist derzeit leer und muss mit weiteren Widgets gefüllt werden, um den Inhalt der App darzustellen.

```dart
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    
    return MaterialApp(
      
      home: Scaffold(
        appBar: AppBar(
          title: Text('Layout einer App'),
        ),
        
        body:
        
        

        ),
      );
  }
}

```

## Vorbereitungen
### Bilder einfügen und Icons verwenden
Im Root Verzeichnis legen sie einen Ordner *assets* an und kopieren drei Bilder (hier verfügbar).

Bearbeitung von *pubspec.yaml*
```dart
flutter:
  assets:
  - assets/berg.jpg
  - assets/stadt.jpg
  - assets/wald.jpg

  uses-material-design: true
```

## Grundlagen

## Bilder anordnen

```dart
Column(
        
          children: [
          
            Row(
            
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              
              children: [
                Expanded(
                  child: Image.asset('assets/berg.jpg'),
                ),

                Expanded(
                  child: Image.asset('assets/stadt.jpg'),
                ),
                
                Expanded(
                  child: Image.asset('assets/wald.jpg'),
                ),
              ],
            ),
        
        Text('test')],

        )


```
## Design nach Widget-Tree
<img src="https://docs.flutter.dev/assets/images/docs/ui/layout/sample-flutter-layout.png">

```dart
Row(
          children: [
            Column(
              children: [
                Icon(Icons.access_alarm,color: Colors.green,),
                Container(child: Text('Test1'),)
                ]),
            Column(
              children: [
                Icon(Icons.star,color: Colors.green,),
                Container(child: Text('Test1'),)
                ]),
            Column(
              children: [
                Icon(Icons.star,color: Colors.green,),
                Container(child: Text('Test1'),)
                ]),
          ],
          ),
```
