# Wasserwaage


In diesem Tutorial möchten wir eine Wasserwaage mit dem eingebauten Lagesensors des Calliope mini programmieren,
um zu prüfen, ob z.B. ein Bild z.B. gerade hängt oder dein Tisch nicht schief steht.

## Step 1

### Variable

Wir fangen mit einer vereinfachten Version der Wasserwaage an, die nur eine Rotationsachse
des Calliope mini berücksichtigt und in einer Bedingung prüft ob ein Schwellenwert von 20 Grad überschritten wurde. In diesem Fall die X-Achse.
Wie bei einer analoge Wasserwaage, wollen wir in diesem Moment die Neigung überprüfen. Daher 
erstellen wir eine Variable in der ``||basic.Dauerschleife||``
mit dem Namen ``||variables.Winkelx.||``,  die immer die derzeitige Neigung speichert.
Setze die Viariable auf ``||input.Rotation (°) Winkel||`` aus den Eingabe-Blöcken, unter ``||input.... mehr||``


```blocks
let Winkelx = 0
basic.forever(function () {
    Winkelx = input.rotation(Rotation.Pitch)
})

```

## Step 2

### Bedingung

Mit einer ``||logic.Wenn/dann||`` Bedingung kann geprüft werden, ob der Schwellewert von 20 Grad überschritten wurde.
Füge aus den ``||logic.Logik||``-Blöcken eine ``||logic.Wenn/dann/ansonsten||``-Bedingung ein mit dem Vergleich ``Winkelx < 20``.

```blocks
let Winkelx = 0
basic.forever(function () {
    Winkelx = input.rotation(Rotation.Pitch)
    if (Winkelx < 20) {
    } else {
    }
})
```

## Step 4

### Vergleiche

Damit die Wasserwaage auch in die andere Drehrichtung funktioniert, können wir 
einen weiteren Vergleich mit dem negativen Winkel hinzufügen  ``Winkelx > -20``
und diese in der Bedingung mit einem ``||logic.und||``-Block verknüpfen

```blocks
let Winkelx = 0
basic.forever(function () {
    Winkelx = input.rotation(Rotation.Pitch)
    if (Winkelx < 20 && Winkelx > -20) {
    } else {
    }
})
```

## Step 5

### LEDs als Rückmeldung

Jetzt brauchen wir nur noch eine Ausgabe, die uns mitteilt, 
wenn der Calliope mini unter 20 Grad geneigt ist. 
Verwende dafür den Block ``||basic.Setzte RGB-LED-Farbe auf||`` aus den Grundlagen und
Setze diese auf grün, wenn der Calliope unter 20 Grad geneigt ist und ansonsten auf rot.


```blocks
let Winkelx = 0
basic.forever(function () {
    Winkelx = input.rotation(Rotation.Pitch)
    if (Winkelx < 20 && Winkelx > -20) {
        basic.setLedColor(0x00ff00)
    } else {
        basic.setLedColor(0xff0000)
    }
})
})
```

## Step 6

### Aufgabe: Hinzufügen der Y-Achse

Klicke auf ||Herunterladen||, um das Programm auf den Mini zu übertrage und zu testen!
Jetzt funktioniert die Wasserwaage für die X-Achse.
Überlege dir, was im Code hinzugefügt werden muss, damit
auch die Neigung Y-Achse überprüft wird. Versuche es erst selbst zu lösen 
und klicke dann auf das Lämpchen, wenn du nicht mehr weiter weißt.

```blocks
basic.forever(function () {
let Winkelx = 0
let Winkely = 0
basic.forever(function () {
    Winkelx = input.rotation(Rotation.Pitch)
    Winkely = input.rotation(Rotation.Roll)
    if (Winkelx < 20 && Winkelx > -20 && (Winkely < 20 && Winkely > -20)) {
        basic.setLedColor(0x00ff00)
    } else {
        basic.setLedColor(0xff0000)
    }
})
})
```

## Step 7

### Wasserwaage für Fortgeschrittene

Da es jetzt schwierig ist X und Y auseinanderzuhalten und wir nicht genau wissen,
in welchem Winkel X und Y-Achse stehen, werden wir an einer 
anderen Lösung für die Ausgabe arbeiten, die allerdings etwas komplizierter ist.
Wir möchte auf der LED-Matrix die X und Y-Position anzeigen.
Wenn der Winkel also von 0° abweicht, dann sich der Punkt von der Mitte nach links
oder rechts verschieben.
Verwende dazu den Block ``||led.Zeichne x 0 y 0||`` aus den LED-Blöcken. 
Entweder du erstellst ein neues Programm oder löscht den anderen Teil, bis auf die Variablen.

```blocks
let Winkelx = 0
let Winkely = 0
basic.forever(function () {
    Winkelx = input.rotation(Rotation.Roll)
    Winkely = input.rotation(Rotation.Pitch)
    led.plot(0, 0)
})
```

## Step 8

### Verteile von bis
Damit der Winkel von -180 bis 180 Grad auf die LEDs von 0 bis 4 übertragen werden, wähle
den Block ``||math.verteile 0 von niedrig bis hoch ...||`` aus ``||math.Mathematik||`` aus.
Verteile den xWinkel von -180 bis 180 zu niedrig 0 zu hoch 4.

```blocks
let x = 0
let y = 0
basic.forever(function () {
    Winkelx = Math.map(input.rotation(Rotation.Roll), -180, 180, 0, 4)
    Winkely = input.rotation(Rotation.Pitch)
    led.plot(0, 0)
})

```

## Step 10

### LED-Punkte zeichnen

Damit die Werte für die LED-Lampen gerade sind, müssen diese noch ``||math.gerundet||`` werden.
Füge die Variable ``||variables.x||`` in ``||led.Zeichne||`` beim x-Wert ein. 
Füge eine **2** für den y-Wert ein, damit die x-Achse mittig von der LED-Matrix positioniert ist.
Klicke auf |Herunterladen|, um das Programm zu testen.

```blocks
let x = 0
let y = 0
basic.forever(function () {
    x = Math.round(Math.map(input.rotation(Rotation.Roll), -180, 180, 0, 4))
    y = input.rotation(Rotation.Pitch)
    led.unplot(x, 2)
})
```

## Step 11

### Zustandsabfrage LED

Vermutlich fiel dir jetzt auf, dass die LED Lampen einmal angeschaltet werden, 
aber danach nicht mehr ausgehen. Das macht es schwierig, die derzeitige Lageposition
abzulesen. Wir müssen also einen Weg finden, wie man erkennt, ob die LED davor
schon angeschaltet ist, bzw. dass diese auch ausgeht, wenn eine Neue angeschaltet wird.
Erstelle dazu eine neue Variable ``||variables.x_davor||`` 
und füge eine ``||logic.Wenn/dann/ansonsten-Bedingung||`` ein
damit wir prüfen können, ob die LED schon angeschaltet wurde.

![alt text](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/variablen.gif)

## Step 12

### Vergleich LED davor

Wir können testen, ob der x Wert der LED innerhalb der Dauerschleife den 
x-Wert verändert hat, indem wir den **X-Wert davor mit dem jetzige x-Wert vergleichen**.
Erstelle dazu den Vergleich: ``||logic.xDavor  ≠ x||`` und füge ihn in die Bedingung ein. 
Falls der x-Wert sich nicht verändert hat, sollen die  "alten LEDs" ``||led.LED ausgeschaltet/gelöscht||`` werden.
``||variables.Setze||`` anschließend die Variable ``||variables.x_davor auf x||``, damit diese immer
wieder nach Änderungen durch den Lagesensor überprüft werden kann.

```blocks
let x = 0
let y = 0
let x_davor = 0
basic.forever(function () {
    x = Math.round(Math.map(input.rotation(Rotation.Roll), -180, 180, 0, 4))
    y = input.rotation(Rotation.Pitch)
    led.plot(x, 2)
    if (x_davor != x) {
        led.unplot(x_davor, 2)
    }
    x_davor = x
})

```

## Step 13

### Aufgabe

Super, für die x-Achse funktioniert es schon ganz gut.
Bisher sind die 180 Grad je Richtung noch ein relativ großer Bereich. Meistens möchten
wir aber nur kleine Abweichungen von wenigen Grad messen: 
1. Überlege, wie die Wasserwaage empfindlicher gemacht werden kann oder nur einen bestimmten
Bereich der Neigung/Drehung berücksichtigt.
2. Stelle genauso wie die X-Achse noch die Y-Achse auf der LED-Matrix dar.

## Step 14

### Ergebnis

**Geschafft!** Klicke auf das Lämpchen für das Ergebnis der finalen Version.  
Jetzt kannst du die Wasserwaage empfindlicher einstellen und schauen
ob dein Tisch gerade steht oder der Boden deines Zuhauses/der Schule eben ist, uvm.!

```blocks
let y_davor = 0
let x_davor = 0
let y = 0
let x = 0
let Maximaler_Winkel = 20
basic.forever(function () {
    x = Math.round(Math.map(input.rotation(Rotation.Roll), Maximaler_Winkel * -1, Maximaler_Winkel, 0, 4))
    y = Math.round(Math.map(input.rotation(Rotation.Pitch), Maximaler_Winkel * -1, Maximaler_Winkel, 0, 4))
    led.plot(x, 2)
    led.plot(2, y)
    if (x_davor != x) {
        led.unplot(x_davor, 2)
    }
    if (y_davor != y) {
        led.unplot(2, y_davor)
    }
    x_davor = x
    y_davor = y
})

```

```template
basic.forever(function () {
})
```