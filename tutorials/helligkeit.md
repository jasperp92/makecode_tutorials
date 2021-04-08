# Wetterstation: Helligkeit

Wir entwickeln in diesem Teil der Wetterstation ein Helligkeitsmessgerät, dass
die LED-Matrix je nach Helligkeit auffüllt.

## Step 1

### Variable für die Helligkeit anlegen.

Als erstens legen wir eine Variable für die Helligkeit an. 
- Erstelle eine ``||variables.Variable||``
- Nenne diese ``Helligkeit``

![alt text](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/variablen.gif)

```template
basic.forever(function () {

})
```

## Step 2

### Helligkeit auslesen

- Verwende den ``||input.Eingabe-Block||``, um die Helligkeit zu messen. 
- Die gemessene Helligkeit sollst du in deine ``||variables.Variable||`` geschrieben werden.

```blocks
let Helligkeit = 0
basic.forever(function () {
    Helligkeit = input.lightLevel()
})
```

## Step 3

### Helligkeit prüfen

Je nach Helligkeit, soll die
LED-Matrix aufgefüllt werden. 
- Ergänze unter dem letzten ``||basic.Zeige Zahl||`` Block eine ``||logic.Wenn/dann||`` Bedingung
- Füge einen logischen Vergleich ein in
denen du prüfst ob die Helligkeit unter 50 liegt.
Dazu wählst du ein aus den Logikblöcken ein ``||logic.<||`` aus, 
und fügst es in die Wenn/dann Bedingung ein.
- Fülle eine LED-Reihe mit ``||basic.zeige die LED||``

```blocks
let Helligkeit = 0
basic.forever(function () {
    Helligkeit = input.lightLevel()
    if (Helligkeit < 51) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . . . . .
            . . . . .
            # # # # #
            `)
    }
})

```

## Step 4

### Aufgabe: Helligkeitsbereiche definieren

Da die ausgelesenen Helligkeitswerte von 0 bis 255 reichen, können wir die 255 durch die 5 LED-Reihen teilen
und bekommen jeweils 51 heraus.

- Berechne die Helligkeitswerte für die anderen Reihen.
- Füge in der Bedingung über das **+** weitere sonst wenn Vergleiche hinzu
und fülle die LED Matrix weiter auf.

*Tipp: Du kannst die LED-Blöcke und Vergleiche einfach mit Strg+C und Strg+V rüberkopieren.*

```blocks
let Helligkeit = 0
basic.forever(function () {
    Helligkeit = input.lightLevel()
    if (Helligkeit < 51) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . . . . .
            . . . . .
            # # # # #
            `)
    } else if (Helligkeit < 102) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . . . . .
            # # # # #
            # # # # #
            `)
    } else if (Helligkeit < 153) {
        basic.showLeds(`
            . . . . .
            . . . . .
            # # # # #
            # # # # #
            # # # # #
            `)
    } else if (Helligkeit < 204) {
        basic.showLeds(`
            . . . . .
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            `)
    } else {
        basic.showLeds(`
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            `)
    }
})

```

## Step 5

### Fertig ist der Helligkeitsmesser!

Klicke auf |Herunterladen|, um das Programm auf deinen Mini zu testen!