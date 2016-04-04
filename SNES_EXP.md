---
layout: page
title: SNES Expansion Bridge
parent: SNES
priority: 2
---

# SNES Expansion Port #

Around late 2014 I started researching the SNES expansion port to see what interesting things could be done through this interface. If one could easily connect homebrew custom peripherals to the console without having to open and modify the internals then this could yield interesting fun projects. The main issue with this interface is its proprietary form factor. 

<center><img src="/public/exp.jpg" style="width: 400px;"/></center>

Facts on this interface:

* It is a 28-pin interface
* It contains a ~1.6mm edge board with the 28 pads
* The interface pitch is measured at 2.00mm from pad to pad

Prior to my work byuu and qwertymodo this research to find modern day connectors to conform to this interface. Unfortunately 2.00mm pitch is not a popular pin pitch and not many companies manufactor a connector that mates to this specification. The one company that did produce connectors at this pin pitch is Samtec with their MEC2 series micro edge connectors. However although the pin pitch was perfect there are no 28-pin variants of this connector to order without placing a very expensive custom order. As a result the solution was to buy the larger MEC2 Samtec connectors and saw off all but the 28 required pins. The part I sourced for my work is the MEC2-30-01-L-DV.

# SNES Expansion Bridge #

Now with a proper connector able to conform with this non-standard interface the next step was to create a conversion board to forward these pins to a more standard connector. After talking with byuu and iterating on a couple different designs we opted for a DB-25 female style connector and two 3.5mm audio barrel connectors for our expansion bridge. I quickly drafted up a design in altium which sources the MEC2 and forwards the signals directly to DB-25. The length of the board was chosen carefully to allow for the expansion bridge to mate to the console and clear the edge for the interfaces to popup next to the native console interfaces. All the digital signals are forwarded to the DB-25 while the analog audio I/O went directly to the audio connectors.

3D Models:
<center><img src="/public/bridge1.png" style="width: 400px;"/></center>
<center><img src="/public/bridge2.png" style="width: 400px;"/></center>
<center><img src="/public/bridge3.png" style="width: 400px;"/></center>

Schematic:
<center><img src="/public/bridge_sch.png" style="width: 12000px;"/></center>

After recieving the green Rev B boards back from fab I was able to successfully test continuity on all pins. I was also successful in testing listening to the mono-out through a normal pair of headphones while also mixing in my iPhone's audio output directly into the SNES line-in stereo input. Everything is function perfectly. Furthermore the length of the board perfectly clear the edge of the console shown by the images below:

<center><img src="/public/bridge4.jpg" style="width: 600px;"/></center>
<center><img src="/public/bridge5.jpg" style="width: 600px;"/></center>
<center><img src="/public/bridge6.jpg" style="width: 600px;"/></center>

Now that we have a perfectly functioning bridge boards we can now create add-on periphals (See 21FX).