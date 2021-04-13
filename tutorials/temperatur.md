# Wetterstation: Temperatur

## Introduction @unplugged

Wir entwickeln in dem ersten Teil der Wetterstation ein Thermometer, dass
die RGB-LED je nach Temperatur in einer anderen Farbe aufleuchten lässt.

## Step 1

### Variable für die Temperatur anlegen.

Als erstens legen wir eine Variable für die Temperatur an. 
- Erstelle eine ``||variables.Variable||``
- Nenne diese ``Temperatur``

![alt text](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/variablen.gif)

```template
basic.forever(function () {

})
```

## Step 2

### Temperatursensor auslesen

Verwende den ``||input.Eingabe-Block||``, um die Temperatur zu messen. Die
gemessene Temperatur sollst du in deine ``||variables.Variable||`` schreiben und den
Wert dann mit einem ``||basic.Zeige Zahl||`` Block ausgeben.

```blocks
let Temperatur = 0
basic.forever(function () {
    Temperatur = input.temperature()
    basic.showNumber(Temperatur)
})
```

## Step 3

### Temperatur prüfen

Jetzt kommt Farbe ins Spiel: Je nachdem welcher Temperatur, soll die
RGB-LED in einer anderen Farbe leuchten.
- Ergänze unter dem letzten ``||basic.Zeige Zahl||`` Block eine ``||logic.Wenn/dann||`` Bedingung
- Füge einen logischen Vergleich ein in
denen du prüfst ob eine Temperatur über oder unterschritten wurde.
Dazu wählst du ein aus den Logikblöcken ein ``||logic.<||`` aus, 
fügst es in die Wenn/dann Bedingung ein.
- Prüfe ob die ``Temperatur < 20`` ist
- ``||basic.Setzte die RGB-Farbe||`` auf blau

```blocks
let Temperatur = 0
basic.forever(function () {
    Temperatur = input.temperature()
    basic.showNumber(Temperatur)
    if (Temperatur < 20) {
    	
    }
})
```

## Step 4

### Aufgabe: Temperaturbereiche definieren

Wenn es kalt ist, soll die LED blau leuchten  
wenn es gemäßigt ist, grün   
wenn es warm ist, gelb  
und wenn es heiß ist, rot.

- Füge in der Bedingung über das **+** weitere sonst wenn Vergleiche hinzu
und lass die LED je nach Temperatur unterschiedlich leuchten.

*Tipp: Du kannst die LED-Blöcke und Vergleiche einfach mit Strg+C und Strg+V rüberkopieren.*

```blocks
let Temperatur = 0
basic.forever(function () {
    Temperatur = input.temperature()
    basic.showNumber(Temperatur)
    if (Temperatur < 20) {
        basic.setLedColor(0x007fff)
    } else if (Temperatur < 25) {
        basic.setLedColor(0x00ff00)
    } else if (Temperatur < 30) {
        basic.setLedColor(0xffff00)
    } else if (Temperatur >= 30) {
        basic.setLedColor(0xff0000)
    }
})
```

## Step 5

### Fertig ist das Thermometer!

Geschafft! Passe gerne die Schwellenwerte nach der Temperatur an, die du auf dem Display siehst,
so dass der Wechsel der LED-Farbe auch bei geringeren Temperaturschwankungen zu sehen ist.

*Wenn die anderen Temperaturbereiche schon abgesteckt sind, kannst du 
die rote LED auch für die Maximaltemperatur, in die ansonsten-Bedingung ohne Vergleich einfügen.
Beides führt zum gleichen Ergebnis!*


```blocks
let Temperatur = 0
basic.forever(function () {
    Temperatur = input.temperature()
    basic.showNumber(Temperatur)
    if (Temperatur < 20) {
        basic.setLedColor(0x007fff)
    } else if (Temperatur < 25) {
        basic.setLedColor(0x00ff00)
    } else if (Temperatur < 30) {
        basic.setLedColor(0xffff00)
    } else {
        basic.setLedColor(0xff0000)
    }
})
```