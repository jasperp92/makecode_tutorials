# Blinkendes Herz

## Introduction @unplugged

Lerne die LED-Matrix zu benutzen, um ein Herz blinken zu lassen!
Learn how to use the LEDs and make a flashing heart! 
(Möchtest du wissen wie LEDs funktionieren? [Schau dieses Video an](https://youtu.be/qqBmvHD5bCw)).


![Heart shape in the LEDs](https://pxt.azureedge.net/blob/4660572a6694f9b6b776367a67d28950f283c929//calliope/tutorials/01_flashing_heart_animation.gif)

## Step 1 @fullscreen

Füge den Block ``||basic.zeige LEDs||``  in den ``||basic.Dauerhaft||``-Block ein und zeichne ein Herz.

![An animation that shows how to drag a block and paint a heart](/calliope/tutorials/add_show_led.gif)

## Step 2 @fullscreen

Füge einen weiteren  ``||basic.zeige LEDs||`` Block ein. Du kannst ihn leer lassen oder reinzeichnen, was du möchtest.

```blocks
basic.forever(function() {
    basic.showLeds(`
        . # . # .
        # # # # #
        # # # # #
        . # # # .
        . . # . .`);
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .`);
})
```

## Step 3 @fullscreen

Schau dir den @boardname@ in der Simulation an. Du solltest dein blinkendes Herz und deine Zeichnung auf dem Bildschirm blinken sehen.

![Heart shape in the LEDs](https://pxt.azureedge.net/blob/4660572a6694f9b6b776367a67d28950f283c929//calliope/tutorials/01_flashing_heart_animation.gif)

## Step 4 @fullscreen

Wenn du einen @boardname@ angeschlossen hast, klicke auf ``|Herunterladen|``, um deinen Code zu übertragen und das Herz blinken zu sehen!