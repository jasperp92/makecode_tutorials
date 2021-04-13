# Wetterstation: Niederschlag

## Introduction @unplugged

In dieser Einheit programmieren wir einen Niederschlagsmesser.  
Um den Niederschlag zu messen und anzuzeigen, wird ein
Auffang- & Messbehälter benötigt, der mit einem Becher, etwas Aluminiumfolie und
Klebeband gebastelt werden kann.

## Step 1

### Start

Beim ``||basic.Start||`` des Programmes soll ein Wassertropfen auf dem Display angezeigt werden.
Zeichne einen Wassertropfen in die LED-Matrix mit ``||basic.Zeige LEDs||``


```blocks
basic.showLeds(`
    . . # . .
    . # # # .
    # # # # #
    # # # # #
    . # # # .
    `)
```

## Step 2

### Wenn/dann/ansonsten Abfrage

Sobald das Wasser den untersten Alustreifen mit dem Minuspol - mit einem
weiteren Alustreifen der an einer Pin angeschlossen ist berührt, wird der Stromkreis
geschlossen und eine Pin gedrückt. Über eine Wenn/dann Abfrage
können wir abfragen, wie hoch das Wasser steht, beziehungsweise welche Pin berührt wurde.
- Füge in die ``||basic.Dauerhaft||``-Schleife eine ``||logic.Wenn/dann/ansonsten||`` Abfrage ein.
- Wähle als Bedingung ``||input.Pin P0 ist gedrückt||`` unter Eingabe aus

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P0)) {
    	
    } else {
    	
    }
})
```
## Step 3

RGB-LED und LED-Matrix 

Wir fragen erst einmal nur die Pin mit dem höchsten Wasserstand ab und 
lassen die anderen aus. Je nachdem, wie du die Pins belegt hast, ist das diejenige
die zum kürzesten Alustreifen führt. Falls es nicht ``P0`` ist, dann ändere die Pin in der Bedingung.
- **Wenn** die Pin gedrückt ist, **dann** ``||basic.zeige eine volle LED-Matrix||``
- **ansonsten**, wenn die Pin nicht berührt ist, dann ``||basic.zeige einen leeren Behälter||`` 

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P0)) {
        basic.setLedColor(0xff0080)
        basic.showLeds(`
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            `)
    } else {
        basic.setLedColor(0xffffff)
        basic.showLeds(`
            # . . . #
            # . . . #
            # . . . #
            # . . . #
            # # # # #
            `)
    }
})

```

## Step 4

Jetzt fügen wir noch die weiteren Alustreifen hinzu und zeichnen den jeweiligen
Wasserstand in die LED-Matrix.
- Klicke 3 mal unten auf das **+** in der Wenn/dann Abfrage, um neue sonst/wenn-Bedingungen hinzuzufügen
- Füge als Bedingung ``||input.Pin ist gedrückt||`` ein und wähle die übrigen Pins aus. Je nach deiner Reihefolge auf- oder absteigend.
- Fülle dort analog zum Niederschalg, die LEDs mit ``||basic.Zeige LEDs||`` auf.

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P0)) {
        basic.setLedColor(0xff0080)
        basic.showLeds(`
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            `)
    } else if (input.pinIsPressed(TouchPin.P1)) {
        basic.showLeds(`
            # . . . #
            # # # # #
            # # # # #
            # # # # #
            # # # # #
            `)
    } else if (input.pinIsPressed(TouchPin.P2)) {
        basic.showLeds(`
            # . . . #
            # . . . #
            # # # # #
            # # # # #
            # # # # #
            `)
    } else if (input.pinIsPressed(TouchPin.P3)) {
        basic.showLeds(`
            # . . . #
            # . . . #
            # . . . #
            # # # # #
            # # # # #
            `)
    } else {
        basic.setLedColor(0xffffff)
        basic.showLeds(`
            # . . . #
            # . . . #
            # . . . #
            # . . . #
            # # # # #
            `)
        basic.turnRgbLedOff()
    }
})
```

## Step 5

### Fertig!
Super, die Programmierung ist geschafft! klicke auf das ``|Herunterladen|``, 
um das Programm auf deinen mini zu spielen und den Niederschlag zu messen.