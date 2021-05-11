# Schrittzähler

## Introduction @unplugged

In diesem Tutorial programmieren wir einen Schrittzähler (Pedometer) mit dem eingebauten
Lagesensor des Calliope mini. 

## Step 1

### Variable erstellen

Als erstes erstellen wir eine Variable, um die Schritte zu hoch zu zählen.

- Lege dazu eine ``||Variables.Variable||`` an mit dem Namen ``Schritte``.
- ``||variables.Setze||`` die Schritte ``||basic.beim Start||`` auf 0.

![Variablen anlegen](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/variablen.gif)

## Step 2

### Schritte messen

Gehen wir davon aus, dass du deinen Calliope mini am Fuß befestigt hast, dann schüttelst
du ihn jedes Mal, wenn du einen Schritt machst. Mit dem Ereignis ``||input.Wenn geschüttelt||``
können wir so den Schritt (in den meisten Fällen) messen. ``||variables.
Ändere||`` die Variable ``||variables.Schritte||`` um 1, wenn der mini geschüttelt wird.

```blocks
let Schritte = 0
Schritte = 0
input.onGesture(Gesture.Shake, function () {
    Schritte += 1
})
```

## Step 3

### Schritte anzeigen lassen

Damit wir wissen wieviele Schritte wir bereits schon gelaufen sind,
können wir uns im ``||basic.Dauerhaft||`` diese mit ``||basic.Zeige Zahl||``
anzeigen lassen.

```blocks
input.onGesture(Gesture.Shake, function () {
    Schritte += 1
})
let Schritte = 0
Schritte = 0
basic.forever(function () {
    basic.showNumber(Schritte)
})
```

## Step 3

### Beschleunigungsensor

Weil das Schüttel-Ereignis relativ grob ist, um leichte Schritte zum messen, werden
wir in dem nächsten Schritt den Beschleunigungsensor verwenden.

- Füge eine ``||logic.wenn/dann||``-Abfrage in die ``||basic.Dauerhaft||``-Schleife ein.
- Verschiebe die ``||variables.Ändere Schritte||`` in die ``||logic.wenn/dann||``-Abfrage
- Den Ereignis-Block ``||input.wenn geschüttelt||`` kannst du löschen.

```blocks
let Schritte = 0
Schritte = 0
basic.forever(function () {
    if (true) {
        Schritte += 1
    }
    basic.showNumber(Schritte)
})

```

## Step 3

### Bedingung für Beschleunigung

Mit jedem Schritt, den du machst beschleunigst du kurz für einen Moment.
Diese Beschleunigung können wir in milli-g messen. Das ist die Einheit für ein Tausendstel der Erdbeschleunigung.
Der Beschleunigungsensor hat drei Achsen. Damit es egal ist, in welche Lage
dein mini ausgerichtet ist, können wir auch die **Stärke** der Beschleunigung auf allen Achsen messen.


- Wähle einen logischen Vergleich aus ``||logic.>||`` aus 
- Füge aus die Beschleunigung aus den Eingabeblöcken und setze diesen auf ``Stärke``

```blocks
let Schritte = 0
Schritte = 0
basic.forever(function () {
    if (input.acceleration(Dimension.X) > 0) {
        Schritte += 1
    }
    basic.showNumber(Schritte)
})
```

## Step 3

### Größe der Beschleunigung

Damit wir nur die Schritte zählen, muss die gemessene Stärke des Beschleunigungssensors höher sein, als die 
Beschleunigung der Erdegraviation von 1000 milli-g oder 1g. 

- Prüfe, ob die Beschleunigung größer ist als eine Zahl, die **über 1000** liegt.
- Klicke auf ``|Herunterladen|`` und prüfe, ob sich der Wert gut eignet, um Schritte zu zählen.

```blocks
let Schritte = 0
Schritte = 0
basic.forever(function () {
    if (input.acceleration(Dimension.X) > 1200) {
        Schritte += 1
    }
    basic.showNumber(Schritte)
})
```

## Step 3

### Anzeige der Schritte

Im letzten Schritt nehmen wir noch eine kleine Änderung vor
damit uns die Schritte, nicht über das Display laufen, wenn diese höher als 10 sind.
Wir lassen uns die letzte Ziffer anzeigen, indem wir den Rest der **Schritte / 10** nehmen.

- Wähle aus Mathematik den ``||math.Rest von||``-Block aus
- ``||basic.Zeige die Zahl||`` aus den Rest der ``||variables.Schritte||`` / 10 an.
- Alle Schritte können wir uns nun anzeigen, ``||input.wenn Knopf A gedrückt||`` wird


```blocks
input.onButtonPressed(Button.A, function () {
    basic.showNumber(Schritte)
})
let Schritte = 0
Schritte = 0
basic.forever(function () {
    if (input.acceleration(Dimension.Strength) > 1200) {
        Schritte += 1
        basic.showNumber(Schritte % 10)
    }
})

```


