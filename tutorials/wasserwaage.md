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

```template
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

### 
Da es jetzt schwierig ist X und Y auseinanderzuhalten
 und auf dem Display das Anzeigen von X und Y-Werten zu lange dauert, arbeiten
 wir an einer anderen Ausgabelösung, die allerdings etwas komplizierter ist.
 Wir möchte auf der LED-Matrix die X und Y-Position darstellen.
