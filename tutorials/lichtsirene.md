# Lichtsirene

## Step 1

Lass die LED nacheinander in verschiedenen Farben leuchten.  
Weil wir eine Sirene bauen möchten die unendlich lange blinkt, müssen die weiteren Blöcke in der ``||basic.dauerhaft||``-Schleife platziert werden.


## Step 2 

Setze die LED auf zwei verschiedene ``Farben`` , indem du zwei mal den Block ``||basic.setze RGB-LED auf||`` hinzufügst.

```blocks
basic.forever(function () {
    basic.setLedColor(0xff0000)
    basic.setLedColor(0x0000ff)
})
```

## Step 3 

Die LED würde jetzt sehr schnell hintereinander blinken, weil es keine Pausen gibt.
``||basic.pausiere||`` den Code jeweils nach dem Wechsel der LED-Farbe.

```blocks
basic.forever(function () {
    basic.setLedColor(0xff0000)
    basic.pause(500)
    basic.setLedColor(0x0000ff)
    basic.pause(500)
})
```

## Step 4 

Super, deine Lichtsirene ist fertig!  
Du kannst gerne die Farben oder auch die Länge der Pausen nach deinem Belieben ändern.
Klicke auf ``|Herunterladen|``, um dein Programm auf deinen Calliope mini zu übertragen!

```template
basic.forever(function () {
})
```