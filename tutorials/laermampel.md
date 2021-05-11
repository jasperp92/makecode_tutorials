# Lärmampel

## Introduction @unplugged

In diesem Tutorial wollen wir mit dem Calliope mini eine Lärmampel programmieren, die uns anzeigt, wenn es zu laut ist. 

## Step 1

### Variable erstellen

Als erstes wollen wir das Geräusch über das eingebaute Mikrofon messen und in einer Variable speicher.
- Erstelle eine Variable mit dem Namen ``||variables.Lautstärke||``
- setze diese in der ``||basic.Dauerhaft||``-Schleife auf ``||input.Lautstärke||`` aus den - Wähle aus den ``||input.Eingabe||``-Blöcken


```blocks
let Lautstaerke = 0
basic.forever(function () {
    Lautstaerke = input.soundLevel()
})
```

## Step 2

### Lautstärke anzeigen lassen

Da wir wissen möchten welche Werte die Lautstärke annehmen kann, können wir uns diese auf der LED-Matrix anzeigen lassen.
- Wähle den Block ``||basic.Zeige Zahl||`` an
- Da die Werte Nachkommastellen haben, kannst du diese auch ``||math.runden||``

```blocks
let Lautstaerke = 0
basic.forever(function () {
    Lautstaerke = input.soundLevel()
    basic.showNumber(Math.round(input.soundLevel()))
})
```


## Step 3

### Schwellenwert definieren

Flüster, schreie oder singe den Calliope mini an und notiere dir, ab welchen Wert es laut oder leise ist.
Wir können mit einer wenn/dann-Abfrage prüfen, wann die Lautstärke einen bestimmten Wert über- oder unterschritten wurde.
- Wähle dazu aus den ``||logic.Logik||``-Blöcken eine ``||logic.wenn/dann/ansonsten||``-Abfrage aus. 
- Füge als Bedingung den logischen Vergleich ein: ``||variables.Lautstärke||`` ``||logic.>||`` dein gemessener Schwellenwert.
- Umgekehrt kannst du natürlich auch mit ``||logic.<||`` prüfen, ob die gemessene Lautstärke leiser ist, als dein Schwellenwert.

```blocks
let Lautstaerke = 0
basic.forever(function () {
    Lautstaerke = input.soundLevel()
    basic.showNumber(Math.round(input.soundLevel()))
    if (Lautstaerke > 80) {
    	
    } else {
    	
    }
})
```

## Step 4

### Ausgabe festlegen

Jetzt legen wir fest, was passiert, wenn es zu laut oder leise ist.
Auf dem Display soll ein glücklicher Smiley angezeigt werden und die RGB-LED grün leuchten, 
wenn es leise ist. Ein trauriger Smiley und eine rote RGB-LED soll angezeigt werden, wenn es zu laut ist.
- Lösche den ersten Block ``||basic.Zeige Zahl||``
- Füge den Block ``||basic.Zeige Symbol||`` und ``||basic.Setze RGB-LED Farbe auf||`` in den richtigen Bereich der wenn/dann-Abfrage ein.


```blocks
let Lautstaerke = 0
basic.forever(function () {
    Lautstaerke = input.soundLevel()
    if (Lautstaerke > 70) {
        basic.showIcon(IconNames.Sad)
        basic.setLedColor(0xff0000)
    } else {
        basic.showIcon(IconNames.Happy)
        basic.setLedColor(0x00ff00)
    }
})
```

## Step 5

### Erweiterung

Super, fertig ist deine Lärmampel.
Wir können die Lärmampel noch um eine Stufe erweitern.
- Klicke dazu auf das **+** in der ``||logic.wenn/dann||``-Abfrage 
- Füge eine weitere Bedingung für die Untergrenze der mittleren Lautstärke ein.
- Füge einen mittelmäßig gelaunten Smiley, als auch eine gelbe RGB-LED hinzu.



```blocks
let Lautstaerke = 0
basic.forever(function () {
    Lautstaerke = input.soundLevel()
    if (Lautstaerke > 70) {
        basic.showIcon(IconNames.Sad)
        basic.setLedColor(0xff0000)
    } else if (Lautstaerke > 30) {
        basic.showLeds(`
            . . . . .
            . # . # .
            . . . . .
            # # # # #
            . . . . .
            `)
        basic.setLedColor(0xffff00)
    } else {
        basic.showIcon(IconNames.Happy)
        basic.setLedColor(0x00ff00)
    }
})

```