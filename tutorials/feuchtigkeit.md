# Wetterstation: Feuchtigkeitsmesser

## Introduction @unplugged

Wir entwickeln in diesem Teil der Wetterstation einen digitalen, als auch analogen Feuchtigkeitsmesser.
Du kannst die Feuchtigkeit entweder über die Pins oder einen Grove Feuchtigkeitssensor messen.
Beide Varianten lassen sich gleich programmieren. (ab Schritt 4)

## Step 1

### Bedingte Anweisung

Um festzustellen, dass die Erde feucht oder trocken ist, können wir über einen Pin messen,
ob der Strom fließt.
- Verwende dazu eine ``||wenn/dann||``-Verzweigung
- Wähle ``||input.Pin P1 ist gedrückt||`` als Bedingung aus

Das ``drücken der Pin`` ist in diesem Fall kein drücken, sondern das schließen
des Stromkreises durch die Erde, da feuchte leitfähiger ist, als trockene Erde.


```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
    } else {
    }
})
```

```template
basic.forever(function () {

})
```

## Step 2

### Bedingung

Wenn die Erde feucht ist, ist alles in Ordnung und ein Smiley wird angezeigt.
Ist die Erde zu trocken, sehen wir einen traurigen Smiley und es gibt einen Warnton,
damit wir an das Gießen erinnert werden.
- Wähle unter ``||basic.Zeige Symbol||`` die beiden Smileys aus und füge sie in die Verzweigung ein.
- ansonsten, wenn die Erde nicht feucht genug ist,  ``||music.Spiele eine Note||``


```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
        basic.showIcon(IconNames.Happy)
    } else {
        basic.showIcon(IconNames.Sad)
        music.playTone(262, music.beat(BeatFraction.Whole))
    }
})
```

## Step 3

### Pause

Damit der Warnton nicht die ganze Zeit hintereinander ausgeführt wird, wenn die Erde zu trocken
ist und in diesem Fall das Programm z.B. nur alle 10 Sekunden prüfen soll, ob die Erde
feucht genug ist, ``||basic.pausieren||`` wir das Programm für 10000 Millisekunden.
Fertig ist der vereinfachte Feuchtigkeitsmesser.
Teste dein Programm:
- Klicke auf |Herunterladen|
- Verbinde den **Minuspin -**, über die Krokodilklemme mit dem einen Nagel in der Erde.
- Verbinde **Pin 0** über die Krokodilklemme mit dem anderen Nagel in der Erde.




```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
        basic.showIcon(IconNames.Happy)
    } else {
        basic.showIcon(IconNames.Sad)
        music.playTone(262, music.beat(BeatFraction.Whole))
    }
basic.pause(10000)
})
```

## Step 4

### Mehrere Zustände

Jetzt wissen wir zwar, ob die erde feucht oder trocken ist, aber wir können nicht
messen, wie feucht diese ist, da digitale Werte nur 2 Zustände annehmen.
Wenn wir analoge Werte auslesen, dann können wir mehrere Abstufungen messen,
wie sehr feucht, mittel und trocken. Die gemessenen Werte reichen von 0 bis 1023.
- Erstelle eine Variable ``||variables.Feuchtigkeit||`` und setze diese auf ``||pin.analoge Werte von Pin P1||``
- Ändere die Bedingung zu ``Feuchtigkeit > 700``
- Klicke auf das **+** in der Verzweigung  und füge eine weitere Bedingung ein, wenn die Erde nur leicht feucht ist.
- ``||basic.Zeige LEDs||`` mit einem Smiley, der weder glücklich noch unzufrieden ist ``:|``

```blocks
let Feuchtigkeit = 0
basic.forever(function () {
    Feuchtigkeit = pins.analogReadPin(AnalogPin.P1)
    if (Feuchtigkeit > 700) {
        basic.showIcon(IconNames.Happy)
    } else if (Feuchtigkeit > 300) {
        basic.showLeds(`
            . . . . .
            . # . # .
            . . . . .
            # # # # #
            . . . . .
            `)
    } else {
        basic.showIcon(IconNames.Sad)
        music.playTone(262, music.beat(BeatFraction.Whole))
    }
    basic.pause(10000)
})

```

## Step 5

### Testen

Super! Dein analoger Feuchtigkeitssensor ist einsatzbereit.
- Verbinde eine Krokodilklemme mit dem **Pluspin +**, damit eine Spannung vom
analogen Pin gemessen werden kann.
- Trage gerne die Grenzwerte in den Bedingungen in eine Tabelle ein
um deinen Sensor anzupassen und zu optimieren, da Faktoren, wie z.B. das Material oder der Abstand zwischen Nägeln die Werte beeinflussen.
- um etwas genauere Ergebnisse zu erzielen, kann z.B. ein **Grove-Sensor** verwendet werden, wofür du lediglich den analogen Pin auf **C16** setzen musst.

