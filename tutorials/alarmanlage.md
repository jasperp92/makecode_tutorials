# Alarmanlage

## Introduction @unplugged

In diesem Tutorial programmieren wir eine Alarmanlage, 
die Alarm schlägt, wenn eine Aktion ausgeführt wird.
Du kannst dir für dieses Projekt gerne überlegen, durch welchen Sensor die Alarmanlage ausgelöst wird.
In unserem Beispiel werden wir den Helligkeitsensor verwenden.

## Step 1

### Helligkeit messen

Zuerst möchten wir nachschauen, wie hell es ist. Die Werte die ausgegeben werden reichen von
0 - 255. Damit wir wissen, ab wann der Wert Helligkeitswert in der Bedingung überschritten ist,
zeigen wir uns diesen an, wenn wir Taste A drücken.
- Füge aus den Eingabe-Blöcken Taste ``||input.wenn Knopf A gedrückt||`` hinzu
- Wähle außerdem noch die ``||input.Lichtstärke||`` aus und zeige diese an, wenn **Knopf B** gedrückt wird mit ``||basic.Zeige Zahl||``
- Lade dein Programm auf den Calliope mini herunter und lese die Werte auf der LED-Matrix. Vergesse nicht Taste A zu drücken!

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showNumber(Helligkeit)
})
```



## step 2

### Ereignis abfragen

Nachdem du nachgeschaut hast wie hell es ist, können wir einen Grenzwert festlegen, ab dem die Alarmanlage in einer wenn/dann-Abfrage ausgelöst wird. 
- Wähle aus den Logik-Blöcken eine ``||logic.Wenn/dann||``-Abfrage aus und füge sie in die ``||basic.Dauerhaft||``-Schleife ein.
- Füge als Bedingung ``Lichtstärke < deinen gemessenen Wert`` ein.
Je nachdem ob die Alarmanlage ausgelöst wird, wenn es heller wird, kannst du auch ein **>** Zeichen einfügen. 
- Füge außerdem 2 Alarmtöne hinzu mit ``||music.Spiele Note||`` 


```blocks
basic.forever(function () {
    if (Helligkeit < 40) {
        music.playTone(262, music.beat(BeatFraction.Whole))
        music.playTone(330, music.beat(BeatFraction.Whole))
    }
})
```

## step 3

### Alarmanlage Scharf schalten - Variablen

Die Alarmanlage funktioniert bisher schon ganz gut. Allerdings möchten wir nicht selbst den Alarm auslösen.
Deshalb werden wir die Alarmanlage noch erweitern, indem wir sie scharf stellen können.

- Erstelle eine Variable mit dem Namen ``angeschaltet`` oder ``scharfgestellt``
- Am Anfang soll die Alarmanlage aus sein. ``||variables.Setzte die Variable||`` im ``||basic.Start||``-Block auf ``falsch``

*Da wir nur zwei Zustände haben, verwendet wir wahr und falsch, du kannst aber auch 0 und 1 verwenden.*

```blocks
scharfgestellt = false
```

## Step 4

### Alarmanlage scharf schalten - LEDs 

Wenn die Alarmanalage aus ist, dann soll die rote LED angeschaltet sein,  
wenn sie angeschaltet ist, eine Grüne. 
- Füge eine neue ``||logic.wenn/dann/ansonsten||``-Abfrage in die ``||basic.Dauerhaft||``-Schleife ein 
- Wähle als Bedingung die Variable ``scharfgestellt`` aus.
- Lass mit ``||basic.Zeige LED||`` die LED rot leuchten, wenn die Alarmanlage angeschaltet ist, ansonsten rot, wenn sie aus ist.

## Step 5

### verschachtelte wenn/dann Abfrage

Nur wenn die Alarmanlage scharfgestellt ist und die Lichtstärke den Schwellenwert unterschritten hat,
dann soll sie auch Alarm schlagen. Wir können einfach zwei wenn/dann Abfragen ineinander verschachtelt.

- Ziehe die erste wenn/dann Abfrage in die den Teil der Zweiten, wenn der Alarm aktiviert ist.

```blocks
basic.forever(function () {
    if (scharfgestellt) {
        basic.setLedColor(0x00ff00)
        if (input.lightLevel() < 20) {
            music.playTone(262, music.beat(BeatFraction.Whole))
            music.playTone(330, music.beat(BeatFraction.Whole))
        }
    } else {
        basic.setLedColor(0xff0000)
    }
})
```

## Step 6

### An- und Ausschalter

Jetzt brauchen wir noch eine Aktion um die Alarmanalge an- und auszuschalten.
Dafür verwenden wir Taste B. Wenn die Alarmanlage aus ist, dann soll diese angeschaltet werden.
Umgekehrt, wenn sie aus ist, an.
- Wähle den Eingabeblock ``||input.wenn Knopf B gedrückt||`` ist aus
- Füge eine ``||logic.wenn/dann/ansonsten||`` Abfrage ein, die prüft, ob die Alarmanlage ``scharfgestellt`` ist
- ``||variables.Setze scharfgestellt||`` auf ``falsch``, wenn sie scharfgestellt ist, ansonsten auf ``wahr``

```blocks
input.onButtonPressed(Button.B, function () {
    if (scharfgestellt) {
        scharfgestellt = false
    } else {
        scharfgestellt = true
    }
})
```

## Step 7

### Geschafft! 

Fertig ist deine Alarmanlage, um dich vor Einbrechern zu schützen!

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showNumber(input.lightLevel())
})
input.onButtonPressed(Button.B, function () {
    if (scharfgestellt) {
        scharfgestellt = false
    } else {
        scharfgestellt = true
    }
})
let scharfgestellt = false
scharfgestellt = false
basic.forever(function () {
    if (scharfgestellt) {
        basic.setLedColor(0x00ff00)
        if (input.lightLevel() < 20) {
            music.playTone(262, music.beat(BeatFraction.Whole))
            music.playTone(330, music.beat(BeatFraction.Whole))
        }
    } else {
        basic.setLedColor(0xff0000)
    }
})
```

