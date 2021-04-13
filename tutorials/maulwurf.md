# Maulwurfspiel

## Introduction @unplugged

Es geht darum, den Maulwurf so schnell wie möglich zu fangen, wenn er aus dem Loch schaut. Auf dem Calliope wird das Auftauchen durch die LEDs (rote Lämpchen) dargestellt. Mit den Knöpfen A und B fangen wir den Maulwurf.

## Step 1

### Die LEDs

Lass zwei LEDs auf der linken Seite des LED-Feldes leuchten und markiere
die Mittellinie auch durch leuchtende LEDs. Platziere dafür 
``||basic.zeige LEDs||`` aus den Grundlagen in den ``||basic.dauerhaft||``-Block.

```blocks
basic.forever(function () {
    basic.showLeds(`
        . . # . .
        # . # . .
        # . # . .
        . . # . .
        . . # . .
        `)
})
```

## Step 2

### Knöpfe drücken

Füge ``||input.wenn Knopf A gedrückt||`` ist und ``||input.wenn Knopf B gedrückt||`` ist hinzu.
In beiden Fällen soll erstmal mit ``||basic.zeige Symbol||`` ein Haken angezeigt werden.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showIcon(IconNames.Yes)
})
input.onButtonPressed(Button.B, function () {
    basic.showIcon(IconNames.Yes)
})
basic.forever(function () {
    basic.showLeds(`
        . . # . .
        # . # . .
        # . # . .
        . . # . .
        . . # . .
        `)
})
```

## Step 3

### Zufall

Jetzt passen wir den Block dauerhaft so
an, dass der Maulwurf zufällig links oder rechts auftaucht.
Lege eine neue ``||variables.Variable||`` an und nenne sie ``Zufall``

![Variablen anlegen](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/variablen.gif)

## Step 4 

### Zufall

Speichere zufällig 0 oder 1 in dem neuen Platzhalter ``Zufall``, indem du aus Variablen ``||variables.ändere Zufall||`` und
aus Mathematik ``||math.wähle eine zufällige Zahl von 0 bis 10||`` verwendest.


```blocks
let Zufall = 0
basic.forever(function () {
    Zufall = randint(0, 1)
    basic.showLeds(`
        . . # . .
        # . # . .
        # . # . .
        . . # . .
        . . # . .
        `)
})
```

## Step 5 

### Wenn-dann

Benutze ``||logic.wenn-dann||`` und ``||logic.=||`` aus Logik und prüfe, ob Zufall = 0 ist. 
Wenn Zufall = 0 ist, dann ist der Maulwurf auf der linken Seite, **ansonsten**
ist er auf der rechten Seite.

```blocks
let Zufall = 0
basic.forever(function () {
    Zufall = randint(0, 1)
    if (Zufall == 0) {
        basic.showLeds(`
            . . # . .
            # . # . .
            # . # . .
            . . # . .
            . . # . .
            `)
    } else if (Zufall == 1) {
        basic.showLeds(`
            . . # . .
            . . # . #
            . . # . #
            . . # . .
            . . # . .
            `)
    }
})
```

## Step 6

### Pause und Geschwindigkeit

``||basic.Pausiere||`` nach dem wenn-dann Block für eine halbe Sekunde (=500 ms),
bevor ein neuer Maulwurf auftaucht. Füge danach mit ``||basic.zeige LEDs||`` nur einen Balken (ohne Maulwurf) ein.  
Probiere aus, was passiert, wenn du die Zeit verringerst.

```blocks
let Zufall = 0
basic.forever(function () {
    Zufall = randint(0, 1)
    if (Zufall == 0) {
        basic.showLeds(`
            . . # . .
            # . # . .
            # . # . .
            . . # . .
            . . # . .
            `)
    } else if (Zufall == 1) {
        basic.showLeds(`
            . . # . .
            . . # . #
            . . # . #
            . . # . .
            . . # . .
            `)
    }
    basic.pause(500)
    basic.showLeds(`
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        `)
})
```

## Step 7

### Variablen lesen
Jetzt prüfen wir, ob der Spieler den richtigen Knopf gedrückt hat.
Wie war das nochmal?  
Wenn **Zufall = 0** ist, dann taucht der Maulwurf **links** auf und wir müssen ihn mit **A**
fangen.  
Wenn **Zufall = 1** ist, dann taucht der Maulwurf **rechts** auf und wir müssen ihn mit **B**
fangen.

```blocks
let Zufall = 0
input.onButtonPressed(Button.A, function () {
    if (Zufall == 0) {
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
input.onButtonPressed(Button.B, function () {
    if (Zufall == 1) {
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
```

## Step 8

### Probier’s aus!

Klasse. Jetzt kannst du schon richtig spielen!  
Klicke auf ``|Herunterladen|``, um dein Programm auf deinen Calliope mini zu übertragen und es auszutesten.
Lass’ uns das Spiel noch erweitern und die gefangenen Maulwürfe mitzählen.  
Wie das geht, siehst du in dem nächsten Schritt.

```blocks
let Zufall = 0
input.onButtonPressed(Button.A, function () {
    if (Zufall == 0) {
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
input.onButtonPressed(Button.B, function () {
    if (Zufall == 1) {
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
basic.forever(function () {
    Zufall = randint(0, 1)
    if (Zufall == 0) {
        basic.showLeds(`
            . . # . .
            # . # . .
            # . # . .
            . . # . .
            . . # . .
            `)
    } else if (Zufall == 1) {
        basic.showLeds(`
            . . # . .
            . . # . #
            . . # . #
            . . # . .
            . . # . .
            `)
    }
    basic.pause(500)
    basic.showLeds(`
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        `)
})

```

## Step 9

### Spielstand
Wir wollen zählen, wie oft wir den Maulwurf gefangen haben. Das können wir mit
einer neuen Variable machen. Erstelle eine neue ``||variables.Variable||`` ``Spielstand`` ``||variables.ändere den Spielstand um 1||``,
wenn der Knopf gedrückt wurde und der Maulwurf auf der richtigen Seite ist.

```blocks
let Zufall = 0
let Spielstand = 0
input.onButtonPressed(Button.A, function () {
    if (Zufall == 0) {
        Spielstand += 1
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
input.onButtonPressed(Button.B, function () {
    if (Zufall == 1) {
        Spielstand += 1    
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
```

## Step 10

### Spielstand anzeigen
Zeige den ``Spielstand`` an, wenn der Calliope geschüttelt wird.


```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(Spielstand)
})
```

## Step 11

### Probier’s aus!
Wow! Jetzt hast du ein richtiges Spiel programmiert, sogar mit Spielstand.  
Um das Spiel noch etwas komplizierter zu machen, hier eine Idee:
Erweitere das Spiel, dass auch zwei Maulwürfe gleichzeitig auftauchen können, die
man mit A+B gleichzeitig fangen muss. Hast du eine Idee, wie das geht?  
Im nächsten Schritt wird es gezeigt.


```blocks
input.onButtonPressed(Button.A, function () {
    if (Zufall == 0) {
        Spielstand += 1
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(Spielstand)
})
input.onButtonPressed(Button.B, function () {
    if (Zufall == 1) {
        Spielstand += 1
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
let Zufall = 0
let Spielstand = 0
Spielstand = 0
basic.forever(function () {
    Zufall = randint(0, 1)
    if (Zufall == 0) {
        basic.showLeds(`
            . . # . .
            # . # . .
            # . # . .
            . . # . .
            . . # . .
            `)
    } else if (Zufall == 1) {
        basic.showLeds(`
            . . # . .
            . . # . #
            . . # . #
            . . # . .
            . . # . .
            `)
    }
    basic.pause(500)
    basic.showLeds(`
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        `)
})
```

## Step 12

### Aufgabe
Wir erweitern das Spiel, sodass auch zwei Maulwürfe gleichzeitig auftauchen
können, die man mit **A+B** fangen muss.
Du musst ein paar Stellen anpassen und einige Blöcke ergänzen.  
**Versuch es erstmal selbst.** 
Wenn du auf das Hinweis-Lämpchen klickst, findest du die Lösung.


```blocks
input.onButtonPressed(Button.A, function () {
    if (Zufall == 0) {
        Spielstand += 1
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
input.onGesture(Gesture.Shake, function () {
    basic.showNumber(Spielstand)
})
input.onButtonPressed(Button.AB, function () {
    if (Zufall == 2) {
        Spielstand += 1
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
input.onButtonPressed(Button.B, function () {
    if (Zufall == 1) {
        Spielstand += 1
        basic.showIcon(IconNames.Yes)
    } else {
        basic.showIcon(IconNames.No)
    }
})
let Zufall = 0
let Spielstand = 0
Spielstand = 0
basic.forever(function () {
    Zufall = randint(0, 2)
    if (Zufall == 0) {
        basic.showLeds(`
            . . # . .
            # . # . .
            # . # . .
            . . # . .
            . . # . .
            `)
    } else if (Zufall == 1) {
        basic.showLeds(`
            . . # . .
            . . # . #
            . . # . #
            . . # . .
            . . # . .
            `)
    } else {
        basic.showLeds(`
            . . # . .
            # . # . #
            # . # . #
            . . # . .
            . . # . .
            `)
    }
    basic.pause(500)
    basic.showLeds(`
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        . . # . .
        `)
})
```
## Step 13

### Glückwunsch

Dein Spiel ist fertig! Toll. Stoppe doch mal die Zeit und schau, wie oft du den
Maulwurf in einer Minute fangen kannst.
Hast du Ideen, wie du das Spiel noch erweitern kannst? Viel Spaß dabei!


```template
basic.forever(function () {
})
```
