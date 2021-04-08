# LED Countdown

## Introduction @unplugged

Wir werden in diesem Tutorial die LEDs mithilfe von Schleifen der Reihe nach 
anschalten und so einen Countdown von 25 Sekunden starten.

## Step 1

### LEDs einzeln anschalten 

``||input.Wenn Knopf A gedrückt||`` wird, soll der Countdown gestartet werden und die LEDs angezeigt werden. 
Wir möchte die LEDs ganz gezielt und einzeln anschalten, deshalb verwenden wir, statt der Grundlagen-Blöcke
die ``||led.LED||``-Blöcke. Füge ``||led.zeichne x 0 y 0 ||`` ein.


```blocks
input.onButtonPressed(Button.A, function () {
    led.plot(0, 0)
})
```

## Step 2

### Schleifen
Um eine Reihe LEDs anzuschalten, können wir den Block kopieren und den x Wert verändern.
Wir können das Programm aber auch kürzen, indem wir eine Schleife verwenden.
Klicke auf ``||loops.Schleifen||`` und wähle den Block ``||loops.für Index von 0 bis 4||`` aus.


```blocks
input.onButtonPressed(Button.A, function () {
for (let Index = 0; Index <= 4; Index++) {
    led.plot(0, 0)
}
})

})
```

## Step 3

### Index zuweisen
Der Index ist eine Variable und taucht jetzt auch unter den ``||variables.Variablen||`` auf.
Der Index wird um einen hochgezählt von 0 bis 4.
Um die LEDs in der Reihe x anzuschalten muss **x** der Variable ``||variables.Index||`` zugewiesen werden.  
*Auch wenn der mini ein 5 x 5 LED-Raster hat wird in einer Reihe nur bis 4 gezählt, weil die 0 mit einbezogen wird.*


```blocks
input.onButtonPressed(Button.A, function () {
for (let Index = 0; Index <= 4; Index++) {
    led.plot(Index, 0)
}
})
})
```

## Step 4

### Countdown
Damit daraus jetzt ein Countdown wird, müssen wir eine Pause einbauen, 
damit die LEDs nach und nach angehen. ``||basic.Pausiere||`` 1 Sekunde in der Schleife, nach dem ``||led.Zeiche||``-Block.
Außerdem soll nach dem Durchlauf der Schleife ein ``||music.Signalton||`` ertönen und die ``||basic.RGB-LED||`` rot leuchten.


```blocks
for (let Index = 0; Index <= 4; Index++) {
    led.plot(Index, 0)
    basic.pause(1000)
}
basic.setLedColor(0xff0000)
music.playTone(262, music.beat(BeatFraction.Whole))
```


## Step 5

### Zwei Wege führen zum Ziel
Damit jetzt in die nächste Reihe gesprungen wird, muss der Y Wert auch hochgezählt werden.
Das kann auf zweierlei Wege geschehen: Über **eine Schleife, die bis 24 zählt** oder über eine **verschachtelte Schleife**.
Beide Wege werden hier vorgestellt. Wir fangen mit der verschachtelten Schleife an.
Füge außen um die erste ``||loops.Schleife||`` eine Weitere hinzu.

```blocks
input.onButtonPressed(Button.A, function () {
    for (let Index = 0; Index <= 4; Index++) {
        for (let Index = 0; Index <= 4; Index++) {
            led.plot(Index, 0)
            basic.pause(1000)
        }
    }
    basic.setLedColor(0xff0000)
    music.playTone(262, music.beat(BeatFraction.Whole))
})
```


## Step 6

### Verschachtelte Schleife
Falls nicht automatisch eine neue Index-Variable angelegt wurde, dann erstelle eine
neue Variable mit dem Namen **y-Index**, damit der Index für die x Reihe nicht der gleiche ist, wie für die y-Reihe.
Klicke mit Rechtsklick auf die ``||variables.Index-Variable||``, um diese in **x-Index** umzubennen.

![index.gif](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/index.gif)

```blocks
input.onButtonPressed(Button.A, function () {
    for (let yIndex = 0; yIndex <= 4; yIndex++) {
        for (let xIndex = 0; xIndex <= 4; xIndex++) {
            led.plot(xIndex, 0)
            basic.pause(1000)
        }
    }
    basic.setLedColor(0xff0000)
    music.playTone(262, music.beat(BeatFraction.Whole))
})
```

## Step 7

### Verschachtelte Schleife
Füge jetzt nur noch die Variable ``||variables.y-Index||`` in das y-Feld von ``||led.Zeichne||`` ein.
Damit der Countdown neu startet, wenn A gedrückt wird,
müssen wir vor dem Start der Schleife den ``||basic.Bildschirminhalt löschen||`` und 
die ``||basic.RGB-LED ausschalten||``.  
**Fertig ist der Countdown!** Im nächsten Schritt wird die zweite Variante vorgestellt. 

```blocks
input.onButtonPressed(Button.A, function () {
    basic.turnRgbLedOff()
    basic.clearScreen()
    for (let yIndex = 0; yIndex <= 4; yIndex++) {
        for (let xIndex = 0; xIndex <= 4; xIndex++) {
            led.plot(xIndex, yIndex)
            basic.pause(1000)
        }
    }
    basic.setLedColor(0xff0000)
    music.playTone(262, music.beat(BeatFraction.Whole))
})
```

## Step 8

### Countdown mit einer Schleife
Statt zwei inneinander verschachtelte Schleifen zu verwenden, 
kann auch eine Schleife verwendet und von 25 heruntergezählt werden. Die X und Y-Werte der LEDs 
errechnen wir uns mathematisch. **Lösche die äußere Schleife** und zähle den Index **0 bis 24** hoch.
Überlege wie du mathematisch auf den Index 0 bis 4 für die X und Y-Werte kommst.


```blocks
input.onButtonPressed(Button.A, function () {
    basic.turnRgbLedOff()
    basic.clearScreen()
        for (let Index = 0; Index <= 24; Index++) {
            led.plot(Index, Index)
            basic.pause(1000)
        }
    basic.setLedColor(0xff0000)
    music.playTone(262, music.beat(BeatFraction.Whole))
})
```

## Step 8

### Countdown mit einer Schleife
Mit der Division des Index durch die Länge Reihe kriegen wir für die Y-Werte heraus:
``0 / 5 = 0, 12 / 5 = 2,4, 24 / 5 = 4,8`` usw.  
Die Nachkommastellen werden von dem ``||led.Zeige||``-Block nicht berücksichtigt und in Ganzzahlen umgewandelt.
Wir können für das bessere Verständnis trotzdem die X-Werte ``||math.abrunden||``.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.turnRgbLedOff()
    basic.clearScreen()
    for (let Index = 0; Index <= 24; Index++) {
        led.plot(Index % 5, 0)
        basic.pause(1000)
    }
    basic.setLedColor(0xff0000)
    music.playTone(262, music.beat(BeatFraction.Whole))
})

```

## Step 9

### Countdown mit einer Schleife
Der Rest der überbleibt, ergibt die X-Werte:  
``0 / 5 = 0 Rest 0, 12 / 5 = 2 Rest 2, 24 / 5 = 4 Rest 4`` usw.  
Verwende dafür den Block ``||math.Rest von||`` aus Mathematik. 

```blocks
input.onButtonPressed(Button.A, function () {
    basic.turnRgbLedOff()
    basic.clearScreen()
    for (let Index = 0; Index <= 24; Index++) {
        led.plot(Index % 5, Math.floor(Index / 5))
        basic.pause(1000)
    }
    basic.setLedColor(0xff0000)
    music.playTone(262, music.beat(BeatFraction.Whole))
})

```

```template
input.onButtonPressed(Button.A, function () {
	
})

```

