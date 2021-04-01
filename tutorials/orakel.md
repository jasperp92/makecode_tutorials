# Orakel

In dieser Einheit wird dein Calliope mini zu einer Wahrsagekugel.  
Schüttle den Calliope mini und du bekommst eine Antwort auf
deine Frage.

## Step 1

Beginne mit dem ``||basic.beim Start||`` Block aus der Kategorie Grundlagen und
füge einen ``||basic.zeige Text||`` Block ein. Ändere den Text in ein Fragezeichen.

```blocks
basic.showString("?")
```

## Step 2

Wähle als nächstes den Block ``||input.wenn geschüttelt||`` in der **Eingabe-
Kategorie** aus. Stelle sicher, dass **geschüttelt** ausgewählt ist.


```blocks
input.onGesture(Gesture.Shake, function () {
	
})
basic.showString("?")
```

## Step 3

Mit dem Block ``||input.Bildschirminhalt löschen||`` kannst du sicher stellen, dass der
Bildschirm aus ist, bevor danach die Gerichte angezeigt werden

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
})
basic.showString("?")
```

## Step 4 

Im nächsten Schritt erstellen wir eine ``||variables.Variable||`` mit dem Namen ``Zufall`` 
und fügen diese in das Event ``||input.wenn geschüttelt||`` ein.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = 0
})
let Zufall = 0
basic.showString("?")
```

## Step 5 

Mithilfe des Blocks ``||math.wähle eine zufällige Zahl||`` aus **Mathematik** kann der Calliope mini
verschiedene Zahlen ausgeben. Füge ihn an den ``||variables.Variable||``-Block in die Schleife.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = randint(0, 10)
})
let Zufall = 0
basic.showString("?")
```

## Step 6

Ändere die **10** zu einer **3** im Zufallsblock, um später eine
Auswahl von vier Gerichten zu treffen. Die **0** zählt mit!

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = randint(0, 3)
})
let Zufall = 0
basic.showString("?")
```

## Step 7

Füge nun einen ``||logic.wenn/dann||`` Bedingung unter dem ``||variables.Zufalls||``-Block ein
und verbinde ihn mit einem Block zum Vergleichen ``||logic.=||`` von zwei Werten. 

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = randint(0, 3)
    if (0 == 0) {
    	
    }
})
let Zufall = 0
basic.showString("?")
```

## Step 8

### Probier’s aus!

Im ersten Programmteil wählt das Programm eine zufällige Zahl und
speichert diese in der Variable **Zufall**. Mit der wenn/dann Bedingung kannst
du den Zahlen Gerichte zuordnen. Füge die Variable ``||variables.Zufall||`` in die Bedingung.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = randint(0, 3)
    if (Zufall == 0) {
    	
    }
})
let Zufall = 0
basic.showString("?")
```

## Step 9

### Spielstand
Mit dem ``||basic.zeige Text||`` Block kannst du nun die erste Antwort in
das Programm aufnehmen und der Zahl **0** zuordnen

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = randint(0, 3)
    if (Zufall == 0) {
        basic.showString("Nudeln mit Pesto")
    }
})
let Zufall = 0
basic.showString("?")
```

## Step 10

Wiederhole die letzten drei Schritte und ordne weitere Essen den Zahlen hinzu, indem du in der wenn/dann Bedingung auf das **+** unten klickst.
Verrgiss nicht die Zahl im Vergleichsblock zu ändern.
*Tipp: Mit Strg+C und Strg+v kannst du ganze Codeblöcke kopieren* 


```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = randint(0, 3)
    if (Zufall == 0) {
        basic.showString("Nudeln mit Pesto")
    } else if (Zufall == 1) {
        basic.showString("Kartoffelbrei mit Apfelmus")
    } else if (Zufall == 2) {
        basic.showString("Reis mit Pilzen")
    } else if (Zufall == 3) {
        basic.showString("Griechischer Salat")
    }
})
let Zufall = 0
basic.showString("?")
```

## Step 11

Super, geschafft! Fertig ist dein Orakel.  
Es macht in diesem Fall übrigens keinen Unterschied, ob du alle 4 Zufallszahlen vergleichst oder nur 3 und das letzte Gericht in die **ansonsten**-Bedingung lässt.



```blocks
input.onGesture(Gesture.Shake, function () {
    basic.clearScreen()
    Zufall = randint(0, 3)
    if (Zufall == 0) {
        basic.showString("Nudeln mit Pesto")
    } else if (Zufall == 1) {
        basic.showString("Kartoffelbrei mit Apfelmus")
    } else if (Zufall == 2) {
        basic.showString("Reis mit Pilzen")
    } else {
        basic.showString("Griechischer Salat")
    }
})
let Zufall = 0
basic.showString("?")
```
