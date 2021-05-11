# Countdown

## Introduction @unplugged

In diesem Tutorial wollen wir mit dem Calliope mini einen Countdown erstellen, der eine Zahl die auf der LED-Matrix anzeigt
herunterzählt.

## Step 1

### Zahlen herunterzählen

Wir fangen mit der einfachen Variante an und lassen uns nacheinander die Zahlen mit einer Pause anzeigen, wenn das Programm gestartet wird.

- Wähle aus den Grundlagen den Block ``||basic.Zeige Zahl||`` und füge diesen in ``||basic.Start||`` ein.
- Füge die Zahl ein von dem der Countdown starten soll.
- Kopiere den Block und zähle weiter runter bis du die 0 erreichst.

*Tipp: Mit Strg+C kannst du Blöcke kopieren und mit Strg+V einfügen.*

```blocks
basic.showNumber(3)
basic.showNumber(2)
basic.showNumber(1)
basic.showNumber(0)
```

## Step 2

### Pausen

Wenn du das Programm auf den Calliope mini testest, dann werden die Zahlen viel zu schnell heruntergezählt.
Deshalb bauen wir dazwischen Pausen ein. Außerdem wollen wir eine grüne LED anschalten, um zu signalisieren, dass der Countdown abgelaufen ist.

- Füge zwischen jedem Block eine 1-sekündige Pause ein mit ``||basic.pausiere||``
- ``||basic.Setze die RGB-LED-Farbe||`` auf grün nach dem letzten Block.

```blocks
basic.showNumber(3)
basic.pause(1000)
basic.showNumber(2)
basic.pause(1000)
basic.showNumber(1)
basic.pause(1000)
basic.showNumber(0)
basic.setLedColor(0x00ff00)
```

## Step 3

### Variablen

Wenn wir die Pausen noch nachträglich ändern wollen, dann müssten wir immer wieder neue Zahlen
in jedes Feld einttippen. In diesem Fall können wir uns die Arbeit erleichtern und eine Variable verwenden.

- Klicke auf ``||variables.Variablen||`` und erstelle eine neue Variable mit dem Namen ``Pause``.
- ``||variables.Setze||`` die Variable bei Start auf die gewünschte Länge der Pause.
- Füge anschließend die gleiche Variable in jede Pause ein. 

```blocks
let Pause = 1000
basic.showNumber(3)
basic.pause(Pause)
basic.showNumber(2)
basic.pause(Pause)
basic.showNumber(1)
basic.pause(Pause)
basic.showNumber(0)
basic.setLedColor(0x00ff00)
```

## Step 4

### Schleifen

Stell dir vor wir wollen jetzt den Countdown von 100 starten. Dann müssten wir sehr oft die Blöcke kopieren und das Programm wird sehr lang.
Mit einer Schleife können wir das Programm flexibel und kurz halten, indem sich wiederholende
Programmelemente nur einmal dargestellt werden.

- Klicke auf ``||loop.Schleifen||`` und erstelle eine neue ``||loop.x-mal wiederholen||``-Schleife
- Füge die sich wiederholenden Blöcke ``||basic.Zeige Zahl||`` und ``||basic.pausiere||`` einmal in die Schleife ein. Die doppelten Blöcke können gelöscht werden.

```blocks
let Pause = 1000
for (let Index = 0; Index <= 4; Index++) {
    basic.showNumber(4)
    basic.pause(Pause)
}
basic.setLedColor(0x00ff00)

```


## Step 5

### Index und Abbruchbedingung

Die meisten Schleifen außer die Dauerhaft-Schleife haben eine Abbruchbedingung. In diesem Fall ist die Abbruchbedingung, wenn
die Zahl 4 erreicht wurde. Solange erhöht die Schleife den Index, bzw. die Zahl, angefangen von 0.
Damit die Zahl des Schleifenindexes angezeigt wird, kannst du die Variable Index
in den Block ``||basic.Zeige Zahl||`` ziehen.

*Du kannst diese sogar auch mit Rechtsklick umbennen und z.B. ``Zahl`` nennen.*

```blocks
let Pause = 1000
for (let Index = 0; Index <= 4; Index++) {
    basic.showNumber(Index)
    basic.pause(Pause)
}
basic.setLedColor(0x00ff00)


```


## Step 6

### Abbruchbedingung

Damit wir den Countdown nicht hoch sondern herunterzählen, können wir den Index von der Startzahl des Countdowns abziehen.
- Erstelle dafür eine neue ``||variables.Variable||`` und benennst diese ``Startzahl``.
- Ziehe mit ``||math.-||`` den Index von der Startzahl ab 

```blocks
let Pause = 1000
let Startzahl = 3
for (let Index = 0; Index <= Startzahl; Index++) {
    basic.showNumber(Startzahl - Index)
    basic.pause(Pause)
}
basic.setLedColor(0x00ff00)
```

