# Stoppuhr

## Introduction @unplugged

Programmiere den Calliope mini als Stoppuhr. 
Miss dazu die Zeit vom ersten Drücken der Taste A bis zum zweiten Drücken der Taste A. 
Zeige diese Zeit in Sekunden am Display an.

## Step 1

### Wie funktioniert eine Stoppuhr?

Im Calliope mini ist eine Uhr eingebaut, aber keine Stoppuhr. 
Überlege, wie du eine Zeit misst, wenn du eine Uhr besitzt, aber keine Stoppuhr. 
Zum Beispiel bei einem Rennen.

```blocks
input.onButtonPressed(Button.A, function () {
	
})
```
## Step 2

### Stoppuhr mit zwei Tasten

In der vereinfachten Version des Programmes
 startest du die Stoppuhr mit der Taste A und stoppst sie mit der Taste B.

Dabei merkt sich der Calliope mini den Zeitpunkt an der die Taste A gedrückt wird. 
Erstelle hierfür eine Variable ``||variables.Startzeit||`` und setze diese auf die ``||input.Laufzeit||``.

![alt text](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/variablen.gif)

```blocks
let Startzeit = 0
input.onButtonPressed(Button.A, function () {
    Startzeit = input.runningTime()
})
```

## Step 3

### Stoppuhr mit zwei Tasten

Durch das ``||input.Drücken der Taste B||`` wird der Stoppvorgang abgeschlossen. 
Ziehe die Startzeit von der aktuellen Laufzeit ab, um die gestoppte Zeit zu erhalten. 

```blocks
let Startzeit = 0
let gestoppte_Zeit = 0
input.onButtonPressed(Button.A, function () {
    Startzeit = input.runningTime()
})
input.onButtonPressed(Button.B, function () {
    gestoppte_Zeit = input.runningTime() - Startzeit
})
```

## Step 4

### Stoppuhr mit zwei Tasten

Zeige nun die gestoppte Zeit mit ``||basic.zeige Zahl||`` auf der LED-Matrix an.
Um die gestoppte Zeit in Sekunden, statt in Millisekunden anzuzeigen, teile die gestoppte Zeit durch 1000.

```blocks
let Startzeit = 0
let gestoppte_Zeit = 0
basic.setLedColor(0x00ff00)
input.onButtonPressed(Button.A, function () {
    basic.setLedColor(0xff0000)
    Startzeit = input.runningTime()
})
input.onButtonPressed(Button.B, function () {
    basic.setLedColor(0x00ff00)
    gestoppte_Zeit = input.runningTime() - Startzeit
    basic.showNumber(gestoppte_Zeit / 1000)
})
```

## Step 5

### Stoppuhr mit zwei Tasten

Damit unterschieden werden kann, ob die Stoppuhr gerade läuft oder nicht, soll 
anhand der ``||basic.RGB-LED||`` erkennbar sein. Sie leuchtet **rot**, wenn die Uhr läuft und **grün**, wenn sie startbereit ist.
Also wird sie auch ``||basic.beim Start||`` auf **grün** gesetzt.
Die Stoppuhr mit zwei Tasten ist fertig! Klicke auf |Herunterladen|, um sie auszutesten.

```blocks
let Startzeit = 0
let gestoppte_Zeit = 0
basic.setLedColor(0x00ff00)
input.onButtonPressed(Button.A, function () {
    basic.setLedColor(0xff0000)
    Startzeit = input.runningTime()
})
input.onButtonPressed(Button.B, function () {
    basic.setLedColor(0x00ff00)
    gestoppte_Zeit = input.runningTime() - Startzeit
    basic.showNumber(gestoppte_Zeit / 1000)
})
```

## Step 6

### Stoppuhr mit einer Taste

Um die Stoppuhr nur mit der Taste A zu bedienen, muss sich der Calliope mini merken,
 ob die Taste A bereits gedrückt wurde. Je nachdem zeigt der mini
  die Zeitdauer an, oder speichert die Startzeit. Mithilfe von Variablen
   merkt sich der mini vergangene Ereignisse. 
   Erstelle eine Variable ``||variables.gestartet||``, die sich merkt, 
   ob die Stoppuhr bereits gestartet wurde und setzte diese beim ``||basic.Start||`` auf **0**.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.setLedColor(0xff0000)
    Startzeit = input.runningTime()
})
input.onButtonPressed(Button.B, function () {
    basic.setLedColor(0x00ff00)
    gestoppte_Zeit = input.runningTime() - Startzeit
    basic.showNumber(gestoppte_Zeit / 1000)
})
let Startzeit = 0
let gestartet = 0
basic.setLedColor(0x00ff00)
```

## Step 7

### Stoppuhr mit einer Taste

Füge in die Bedingung ``||logic.Wenn gestartet = 0||`` den Programmteil, 
der beim Start des Stoppvorgang passiert ein. 
Im Bereich ``||logic.ansonsten||`` den Programmteil, der beim Ende des Stoppvorgang passiert.  
*Tipp: Die Blöcke können mit **Strg+C** und **Strg+V** aus dem ``||variables.wenn Knopf B gedrückt||`` wird in den ``||logic.ansonsten||``-Teil kopiert werden.* 

```blocks
input.onButtonPressed(Button.A, function () {
    if (gestartet == 0) {
        basic.setLedColor(0xff0000)
        Startzeit = input.runningTime()
    } else {
        basic.setLedColor(0x00ff00)
        gestoppte_Zeit = input.runningTime() - Startzeit
        basic.showNumber(gestoppte_Zeit / 1000)
    }
})
let gestoppte_Zeit = 0
let Startzeit = 0
let gestartet = 0
gestartet = 0
basic.setLedColor(0x00ff00)
```

## Step 8

### Stoppuhr mit einer Taste

Stelle diese Variable ``||variables.gestartet||`` auf **1** wenn die Stoppuhr 
 gestartet wurde und stelle sie auf **0** 
nach Ende des Stoppvorgang, damit das Programm neu startet.

```blocks
input.onButtonPressed(Button.A, function () {
    if (gestartet == 0) {
        basic.setLedColor(0xff0000)
        Startzeit = input.runningTime()
        gestartet = 1
    } else {
        basic.setLedColor(0x00ff00)
        gestoppte_Zeit = input.runningTime() - Startzeit
        basic.showNumber(gestoppte_Zeit / 1000)
        gestartet = 0
    }
})
let gestoppte_Zeit = 0
let Startzeit = 0
let gestartet = 0
gestartet = 0
basic.setLedColor(0x00ff00)
```

## Step 9

### Stoppuhr mit einer Taste  - Kurzer Code

Super. Die Stoppuhr ist fertig. Zu guter Letzt kann der Code noch verkürzt werden, 
indem die Variabel ``||Startzeit||`` auch prüft, ob die Uhr gerade läuft oder nicht.

```blocks
input.onButtonPressed(Button.A, function () {
    if (Startzeit == 0) {
        basic.setLedColor(0xff0000)
        Startzeit = input.runningTime()
    } else {
        basic.setLedColor(0x00ff00)
        gestoppte_Zeit = input.runningTime() - Startzeit
        basic.showNumber(gestoppte_Zeit / 1000)
        Startzeit = 0
    }
})
let gestoppte_Zeit = 0
let Startzeit = 0
Startzeit = 0
basic.setLedColor(0x00ff00)
```

```template
input.onButtonPressed(Button.A, function () {
	
})

```

