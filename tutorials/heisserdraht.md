# Heißer Draht

Beim Spiel „Der heiße Draht“ führen die Schüler*innen einen Spielstab entlang 
einer Bahn aus Draht, ohne den Draht zu berühren. 
Passiert es doch, wird dies durch ein Licht-oder Tonsignal gemeldet. 
Dazu programmieren die Schüler*innen den Calliope mini.

## Step 1

### Wenn/dann-Verzweigung für Berührung

Da wir abfragen möchten, ob der Stromkreis zwischen Minuspol und P1 geschlossen wird, brauchen wir eine Wenn-/dann-Bedingung.
Allerdings verwenden wir nicht den Eventblock ``||input.wenn Pin P0 gedrückt||``, sondern erstellen eine eigene Abfrage, um auch ein "ansonsten"-Bedingung setzen zu können.
Verwende dazu aus den Logik-Bausteinen den ``||logic.wenn, dann||``-Block und füge die Bedingung ``||input.Pin P1 ist gedrückt||`` ein.

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P0)) {
    } else {
    }
})
```

## Step 2

### Rückmeldung bei Berührung

Nun möchten wir den eine die RGB-LED rot aufleuchten lassen und ein Tonsignal abspielen und ein ``X`` auf der LED-Matrix anzeigen lassen, wenn der Draht berührt wird.
Falls dieser nicht berührt wird, soll die LED grün leuchten.

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P0)) {
        basic.setLedColor(0xff0000)
        basic.showIcon(IconNames.No)
        music.playTone(262, music.beat(BeatFraction.Whole))
        basic.clearScreen()
    } else {
        basic.setLedColor(0x00ff00)
    }
})
```

## Step 3

### Variablen

Prima, jetzt hast du das Grundgerüst des Spiels schon fertig.
Wir wollen dem Spiel noch ein Punktesystem hinzufügen und zwei weitere Pins verwenden, um Start und Stopp der Drahtbahn zu erfassen.
Zu allererst erstellen wir zwei Variablen. Eine für das Punktesystem und eine für die Abfrage, ob das Spiel gestartet wurde.  
Klicke auf ``||variables.Variablen||`` und erstelle zwei mit den Namen ``Berührungen`` und ``Spielstart``.

![alt text](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/variablen.gif)

## Step 4 

### Variablen

Setze die Variablen in die ``||basic.beim Start||``-Funktion ein.
Weil das Spiel nur zwei Zustände einimmt, wie ``Spielstart`` und ``Spielende``, können wir einen 
Wahrheitswert in die Variable aus dem ``||logic.Logik||``-Block einfügen. Setze diese auf ``wahr``.


```blocks
let Spielstart = false
let Berührungen = 0
Berührungen = 0
Spielstart = true
```

## Step 5 

### Berührungen zählen

In dem nächsten Schritt möchten wir einen Zähler einbauen, jedesmal wenn wir den heißen Draht berühren, beziehungsweise Pin 1 gedrückt wurde.
Wähle aus den ``||variable.Variablen||`` den Block ``||variable.ändere Berührung um 1||`` aus.

```blocks
input.onPinPressed(TouchPin.P0, function () {
    Berührungen += 1
    basic.setLedColor(0xff0000)
    basic.showString("C")
    music.playTone(262, music.beat(BeatFraction.Quarter))
    basic.turnRgbLedOff()
    basic.clearScreen()
})
```

## Step 6

### Abfrage Spielende

Wenn das Spiel beendet ist, möchten wir die Berührungen angezeigt haben. Dafür brauchen wir eine weitere ``||logic.Wenn/dann-Verzweigung||``, die prüft, ob der Spielstart ``wahr`` oder ``falsch`` ist.
Baue deinen bisherigen Code in den oberen Bereich ein, wenn das Spiel gestartet ist. Ansonsten wenn das Spiel beendet ist, ``||input.zeige die Zahl||`` der ``||variables.Berührungen||``.

## Step 7

### Bedingungen für das Spielende
Wir haben noch kein Ereignis, dass Start und Ende des Spiels bestimmt. 
Dafür verwenden wir zwei weitere Pins, die den Stromkreis am Anfang und Ende schließen.
Da es kein Verhalten für Ansonsten gibt, kannst du zwei Eventblöcke ``||input.wenn Pin P0 gedrückt||`` verwenden und setzt die Pins auf ``P0`` und ``P2``.

```blocks
input.onPinPressed(TouchPin.P2, function () {
})
input.onPinPressed(TouchPin.P1, function () {
})
```

## Step 8

### Spielstart und -Ende zuweisen

Fast geschafft! Weise die Variable Spielstart noch dem richtigen Ereignis zu.
P1 ist der Auslöser am Anfang des Drahtes und setzt den Spielstart auf ``wahr``.
Dabei wird die Punktzahl auf 0 gesetzt und der Bildschirm gelöscht.
P2 ist der Auslöser am Ende des Drahtes und setzt den Spielstart auf ``falsch``. Also ist das Spiel vorbei. Dabei sollen die RGB-LED auch ausgeschaltet werden.
Versuche die Blöcke selbst zu finden und einzubauen.

```blocks
input.onPinPressed(TouchPin.P2, function () {
    Spielstart = false
    basic.turnRgbLedOff()
})
input.onPinPressed(TouchPin.P1, function () {
    Spielstart = true
    Berührungen = 0
    basic.clearScreen()
})
```

## Step 9

### Fertig! 
Geschafft, die Programmierung ist fertig! 
Klicke auf ``|Herunterladen|``, um dein Programm auf deinen Calliope mini zu übertragen und Klavier zu spielen.

```blocks
input.onPinPressed(TouchPin.P2, function () {
    Spielstart = false
    basic.turnRgbLedOff()
})
input.onPinPressed(TouchPin.P1, function () {
    Spielstart = true
    Berührungen = 0
    basic.clearScreen()
})
let Spielstart = false
let Berührungen = 0
Berührungen = 0
Spielstart = true
basic.forever(function () {
    if (Spielstart) {
        if (input.pinIsPressed(TouchPin.P0)) {
            Berührungen += 1
            basic.setLedColor(0xff0000)
            basic.showIcon(IconNames.No)
            music.playTone(262, music.beat(BeatFraction.Half))
            basic.clearScreen()
        } else {
            basic.setLedColor(0x00ff00)
        }
    } else {
        basic.showNumber(Berührungen)
    }
})

```

## Step 10

### Spielaufbau

Du kannst du dich an den Aufbau machen, falls du es nicht schon vor der Programmierung erledigt hast.
Dazu findest du hier einen groben Aufbauplan.
Viel Spaß!

![Aufbauplan](https://raw.githubusercontent.com/jasperp92/makecode-tutorials/master/assets/images/bauplan.png)