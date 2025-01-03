---
title: "Python - Vuurwerk"
date: 2025-01-02T19:51:01+02:00
draft: false
toc: true
headercolor: "teal-background"
onderwerp: Python 
---

Dit is de eerste dojo in het nieuwe jaar 2025 en we maken deze keer vuurwerk!

<!--more-->

![Happy new year](happy-new-year.gif)

Bij oud en nieuw hoort vuurwerk, dus deze keer maken we met Python en de Turtle bibliotheek zelf ons vuurwerk.

Deze instructie is vrij uitgebreid en maakt gebruik van technieken die onbekend zijn voor beginners. Maar, als de
code goed wordt gekopieerd en plakt, moet het lukken iets werkends te krijgen zonder dat je precies begrijpt hoe het
werkt.  
En vergeet vooral geen hulp te vragen aan de mentoren. 😉

## Thonny installeren

{{< include file="installatie/thonny.md" >}}

## 🎆 Vuurwerk maken!

We beginnen met het maken van een vuurpijl die de lucht in schiet. Dat gaan we in stappen doen:

### 1. We maken een window
Neem het volgende over in Thonny:
```python
import turtle

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)
```

![Thonny scherm](plaatjes/thonny-scherm.png)  

Druk op het groene knopje of F5 om het programma uit te proberen. 
![Thonny uitvoerknop](plaatjes/thonny-uitvoerknop.png)

**Let op!** als je het window niet met het kruisje rechts boven af kunt sluiten, gebruik dan de rode stopknop in Thonny. 


### 2. En een zwarte punt dat later de pijl wordt

```python
import turtle

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

vuurpijl = turtle.Turtle()
vuurpijl.dot(5)
```
Voer het programma uit. Zie je de zwarte punt?

### 3. De vuurpijl beweegt omhoog
Laten we eens kijken of we de punt naar boven kunnen laten bewegen.
```python
import turtle

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

vuurpijl = turtle.Turtle()
vuurpijl.dot(5)
vuurpijl.setposition(0, 50)
vuurpijl.dot(5)
```
Als je dit uitvoert, zie je twee punten met een dunne lijn er tussen. Dat is niet helemaal wat we willen.
Eigenlijk willen we dat de punt beweegt.

### 4. De vuurpijl beweegt nu echt omhoog
```python
import turtle

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

vuurpijl = turtle.Turtle()

for i in range(10):
    vuurpijl.clear()
    vuurpijl.setposition(0, 15 * i)
    vuurpijl.dot(5)
```
Staat de punt nog in het midden? Heb je het zien bewegen?

- Met `for i in range(10):` herhalen we de 3 ingesprongen regels eronder 10 keer
- `vuurpijl.clear()` verwijdert de laatst getekende punt, zodat je alleen de nieuwe, verschoven punt ziet
- `vuurpijl.setposition(0, 15 * i)` plaatst de punt, hierbij bepaald:
  - `0` de horizontale positie, waarbij 0 in het midden van het window is
  - `15 * i` de verticale positie, waarbij ook hier 0 in het midden van het window is; door 15 x i te gebruiken 
    verschuift de punt wat verder naar boven dan alleen met i; overigens verandert i van 0 tot en met 9 met de herhaling

Wat gebeurt er als je de horizontale positie veranderd? Dus de 0 in `vuurpijl.setposition(0, 15 * i)` veranderd in 40 of -40?

### 5. En nu dat je de vuurpijl echt ziet bewegen
```python
import turtle
from time import sleep

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

vuurpijl = turtle.Turtle()
vuurpijl.hideturtle()

for i in range(100):
    vuurpijl.clear()
    vuurpijl.setposition(0, 3*i)
    vuurpijl.dot(5)
    window.update()
    sleep(0.1)
```
Je kunt de pijl nu echt zien bewegen, doordat

- er meer stappen worden gezet
- er tussen iedere stap even wordt gewacht door het `sleep(0.1)` commando

Wat gebeurt er als je het aantal stappen verandert door 100 in `range(100)` te vervangen door 50 of juist 150?  
Of wanneer je het getal in `sleep(0.1)` verandert van 0.1 naar 0.02 of juist 0.2?  
Of wanneer je het getal 3 in `vuurpijl.setposition(0, 3*i)` verandert naar 2 of 5?

### 6. Een pijl beweegt meestal niet recht naar boven

We hebben in stap 4 gezien dat het aanpassen van de 0 in `vuurpijl.setposition(0, 3*i)` de horizontale positie van de
pijl veranderd. Maar een pijl beweegt meestal niet recht naar boven, maar eerder wat schuin:

```python
import turtle
from time import sleep

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

vuurpijl = turtle.Turtle()
vuurpijl.hideturtle()

for i in range(100):
    vuurpijl.clear()
    vuurpijl.setposition(i, 5*i)
    vuurpijl.dot(5)
    window.update()
    sleep(0.1)
```
Je ziet nu dat de pijl naar rechts boven verplaatst. Dit komt doordat we 0 met i hebben vervangen in 
`vuurpijl.setposition(0, 5*i)`.

Wat gebeurt er nu als je `-i` gebruikt?  
Of `-2 * i`?

### 7. Voorbereiden voor meerdere pijlen

Om zo makkelijker met meerdere pijlen te kunnen werken, moeten we de code even aanpassen:

```python
import turtle
from time import sleep

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

class Vuurpijl:
    def __init__(self):
        self.turtle = turtle.Turtle()
        self.turtle.hideturtle()
        self.plaats_horizontaal = 0
        self.plaats_verticaal = 0
        self.snelheid_horizontaal = 1
        self.snelheid_verticaal = 3
        
    def beweeg(self):
        self.plaats_verticaal = self.plaats_verticaal + self.snelheid_verticaal
        self.plaats_horizontaal = self.plaats_horizontaal + self.snelheid_horizontaal
        self.turtle.clear()
        self.turtle.setposition(self.plaats_horizontaal, self.plaats_verticaal)
        self.turtle.dot(5)

vuurpijl = Vuurpijl()
for i in range(100):
    vuurpijl.beweeg()
    window.update()
    sleep(0.02)
```
Als je dit hebt uitgevoerd, zie je dat het nog steeds hetzelfde doet als bij stap 7. Dus wat is er nu eigenlijk 
veranderd en waarom?

- allereerst is de vuurpijl code in een "class" gestopt. Een class beschrijft de eigenschappen en gedrag van de vuurpijl.
  - in functie `__init__(self)` worden een aantal begin eigenschappen bepaald, zoals de horizontale en verticale plaats
    en snelheid
  - in functie `beweeg(self)` staat het gedrag van de vuurpijl. Bij iedere aanroep worden de horizontale en verticale
    plaats bepaald door er de horizontale en verticale snelheden bij op te tellen. Dan wordt de positie van de vuurpijl
    gezet met `self.turtle.setposition(self.plaats_horizontaal, self.plaats_verticaal)` en tenslotte getekend met
    `self.turtle.dot(5)`. 
- dan wordt er een "instantie" van de class Vuurpijl gemaakt: `vuurpijl = Vuurpijl()`. `vuurpijl` is nu een object van
  class `Vuurpijl` en heeft het gedrag van `Vuurpijl`. Door functie `vuurpijl.beweeg()` aan te roepen, gaat de vuurpijl
  bewegen.

Speel eens met de waarden van `self.plaats_horizontaal`, `self.plaats_verticaal`, `self.snelheid_horizontaal`, 
`self.snelheid_verticaal`?  
Kun je de pijl ook van rechts boven in het window naar links onder laten bewegen? Wat moet daarvoor veranderen?

### 8. Fijn, die voorbereiding, nu wil ik meerdere pijlen!

```python
import turtle
from time import sleep

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

class Vuurpijl:
    def __init__(self):
        self.turtle = turtle.Turtle()
        self.turtle.hideturtle()
        self.plaats_horizontaal = 0
        self.plaats_verticaal = 0
        self.snelheid_horizontaal = 1
        self.snelheid_verticaal = 3
        
    def beweeg(self):
        self.plaats_verticaal = self.plaats_verticaal + self.snelheid_verticaal
        self.plaats_horizontaal = self.plaats_horizontaal + self.snelheid_horizontaal
        self.turtle.clear()
        self.turtle.setposition(self.plaats_horizontaal, self.plaats_verticaal)
        self.turtle.dot(5)

vuurpijl1 = Vuurpijl()
vuurpijl2 = Vuurpijl()
for i in range(100):
    vuurpijl1.beweeg()
    vuurpijl2.beweeg()
    window.update()
    sleep(0.02)
```

Zie je `vuurpijl1` en `vuurpijl2`? Dat is alles wat er nodig is om 2 vuurpijlen te maken. Super handig!

Maar zie je ook 2 pijlen? Hoe zou het kunnen dat je er maar 1 ziet?

### 9. Nu echt meerdere pijlen!

Doordat bij stap 8 de 2 pijlen beiden op dezelfde plaats beginnen en precies dezelfde kant op gaan met dezelfde snelheid,
kun je niet zien dat het er echt 2 zijn.  
Om dit op te lossen kunnen de code aanpassen zodat we voor iedere pijl de horizontale en verticale snelheid kunnen
meegeven:

```python
import turtle
from time import sleep

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)

class Vuurpijl:
    def __init__(self, snelheid_horizontaal, snelheid_verticaal):
        self.turtle = turtle.Turtle()
        self.turtle.hideturtle()
        self.plaats_horizontaal = 0
        self.plaats_verticaal = 0
        self.snelheid_horizontaal = snelheid_horizontaal
        self.snelheid_verticaal = snelheid_verticaal
        
    def beweeg(self):
        self.plaats_verticaal = self.plaats_verticaal + self.snelheid_verticaal
        self.plaats_horizontaal = self.plaats_horizontaal + self.snelheid_horizontaal
        self.turtle.clear()
        self.turtle.setposition(self.plaats_horizontaal, self.plaats_verticaal)
        self.turtle.dot(5)

vuurpijl1 = Vuurpijl(-1, 3)
vuurpijl2 = Vuurpijl(0, 3)
vuurpijl3 = Vuurpijl(1, 3)
for i in range(100):
    vuurpijl1.beweeg()
    vuurpijl2.beweeg()
    vuurpijl3.beweeg()
    window.update()
    sleep(0.02)
```
![3 vuurpijlen](plaatjes/3-vuurpijlen.gif)

Wat is er veranderd?

- functie `__init__` heeft argumenten `snelheid_horizontaal` en `snelheid_verticaal` gekregen, waardoor je iedere 
  vuurpijl een andere richting en snelheid kunt geven
- er zijn nu 3 vuurpijlen met verschillende snelheden. Je ziet dat pijl 1 een horizontale snelheid -1 heeft. Deze beweegt
  naar links. Pijl 2 heeft 0 en beweegt recht naar boven en pijl 3 met horizontale snelheid 1 beweegt naar rechts

Speel eens met de waarden voor de vuurpijlen en kijk wat er gebeurd? 

Wat gebeurt er als je dit gebruikt? Vergeet je niet `vuurpijl4` ook te laten bewegen?

```python
vuurpijl1 = Vuurpijl(1, 3)
vuurpijl2 = Vuurpijl(-1, 3)
vuurpijl3 = Vuurpijl(1, -3)
vuurpijl4 = Vuurpijl(-1, -3)
```

### 10. Dit lijkt helemaal niet op vuurwerk!

Klopt! We hebben wat voorbereidend werk moeten doen en gaan nu eens kijken of we het meer op vuurwerk kunnen laten
lijken.

```python
import turtle
from time import sleep

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)
window.bgcolor("black")

class Vuurpijl:
    def __init__(self, snelheid_horizontaal, snelheid_verticaal):
        self.turtle = turtle.Turtle()
        self.turtle.hideturtle()
        self.turtle.color("gold")
        self.plaats_horizontaal = 0
        self.plaats_verticaal = -390
        self.snelheid_horizontaal = snelheid_horizontaal
        self.snelheid_verticaal = snelheid_verticaal
        
    def beweeg(self):
        self.plaats_verticaal = self.plaats_verticaal + self.snelheid_verticaal
        self.plaats_horizontaal = self.plaats_horizontaal + self.snelheid_horizontaal
        self.turtle.clear()
        self.turtle.setposition(self.plaats_horizontaal, self.plaats_verticaal)
        self.turtle.dot(5)

vuurpijl1 = Vuurpijl(1, 3)
vuurpijl2 = Vuurpijl(-1, 3)
vuurpijl3 = Vuurpijl(0, 3)
vuurpijl4 = Vuurpijl(0.5, 3)
for i in range(200):
    vuurpijl1.beweeg()
    vuurpijl2.beweeg()
    vuurpijl3.beweeg()
    vuurpijl4.beweeg()
    window.update()
    sleep(0.02)
```
![4 vuurpijlen op een zwarte achtergrond](plaatjes/4-vuurpijlen-zwarte-achtergrond.gif)

### 11. Meer pijlen! Ik wil meer pijlen!

Met alle werk dat we hebben gedaan, kunnen we nu makkelijk nog meer pijlen toevoegen:

```python
import turtle
from time import sleep
from random import randint

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)
window.bgcolor("black")

class Vuurpijl:
    def __init__(self, snelheid_horizontaal, snelheid_verticaal):
        self.turtle = turtle.Turtle()
        self.turtle.hideturtle()
        self.turtle.color("gold")
        self.plaats_horizontaal = 0
        self.plaats_verticaal = -390
        self.snelheid_horizontaal = snelheid_horizontaal
        self.snelheid_verticaal = snelheid_verticaal
        
    def beweeg(self):
        self.plaats_verticaal = self.plaats_verticaal + self.snelheid_verticaal
        self.plaats_horizontaal = self.plaats_horizontaal + self.snelheid_horizontaal
        self.turtle.clear()
        self.turtle.setposition(self.plaats_horizontaal, self.plaats_verticaal)
        self.turtle.dot(5)

vuurpijlen = []
for _ in range(10):
    vuurpijlen.append(Vuurpijl(randint(-15, 15)/10, randint(20, 30)/10))

for i in range(200):
    for vuurpijl in vuurpijlen:
        vuurpijl.beweeg()
    window.update()
    sleep(0.02)
```

![10 vuurpijlen in verschillende richtingen](plaatjes/10-vuurpijlen-verschillende-richtingen.gif)

Hier zitten de belangrijke wijzigingen:

```python
vuurpijlen = []
for _ in range(10):
    vuurpijlen.append(Vuurpijl(randint(-15, 15)/10, randint(20, 30)/10))

for i in range(200):
    for vuurpijl in vuurpijlen:
        vuurpijl.beweeg()

```

- `vuurpijlen = []`: allereerst maken een we een lijst aan waarin we de vuurpijlen bewaren
- `for _ range(10):`: dan voegen we 10 pijlen aan het lijstje toe
- functie `randint(-15, 15)` geeft zomaar een getal tussen -15 en 15 terug, dus bij een eerste aanroep bijvoorbeeld 3, 
  maar bij een volgende -4 en dan weer 9. Hierdoor kunnen we ervoor zorgen dat de pijlen met verschillende horizontale
  en verticale snelheden gaan bewegen.  
  We delen het resultaat door 10, omdat `randint` alleen maar gehele getallen teruggeeft, dus geen komma getallen zoals
  1.5. -15 tot +15 zou een veel te grote horizontale snelheid opleveren en de pijlen links en rechts uit het window laten 
  vliegen. `randint(-15, 15)/10` levert getallen op tussen -1.5 en +1.5 wat beter werkt.
- tenslotte halen we met `for vuurpijl in vuurpijlen:` één voor één de vuurpijlen uit het lijstje en roepen de 
  `vuurpijl.beweeg()` functie aan om de pijlen een stap te laten maken.

### 12. Maar vuurpijlen vallen toch weer naar beneden?

Dat klopt. De zwaartekracht zorgt ervoor dat de vuurpijlen afremmen, tot stilstand komen en dan weer naar beneden vallen:

![vuurpijlen met zwaartekracht](plaatjes/vuurpijlen-met-zwaartekracht.gif)

```python
import turtle
from time import sleep
from random import randint

window = turtle.Screen()
window.setup(800, 800)
window.tracer(0)
window.bgcolor("black")

class Vuurpijl:
    def __init__(self, snelheid_horizontaal, snelheid_verticaal):
        self.turtle = turtle.Turtle()
        self.turtle.hideturtle()
        self.turtle.color("gold")
        self.plaats_horizontaal = 0
        self.plaats_verticaal = -390
        self.snelheid_horizontaal = snelheid_horizontaal
        self.snelheid_verticaal = snelheid_verticaal
        self.zwaartekracht = 0.06
        
    def beweeg(self):
        self.plaats_verticaal = self.plaats_verticaal + self.snelheid_verticaal
        self.plaats_horizontaal = self.plaats_horizontaal + self.snelheid_horizontaal
        self.snelheid_verticaal = self.snelheid_verticaal - self.zwaartekracht
        self.turtle.clear()
        self.turtle.setposition(self.plaats_horizontaal, self.plaats_verticaal)
        self.turtle.dot(5)

vuurpijlen = []
for _ in range(10):
    vuurpijlen.append(Vuurpijl(randint(-15, 15)/10, 6 + randint(20, 30)/10))

for i in range(300):
    for vuurpijl in vuurpijlen:
        vuurpijl.beweeg()
    window.update()
    sleep(0.02)

```

Met de belangrijkste wijzigingen:

```python
class Vuurpijl:
    def __init__(self, snelheid_horizontaal, snelheid_verticaal):
        self.zwaartekracht = 0.06
        
    def beweeg(self):
        self.snelheid_verticaal = self.snelheid_verticaal - self.zwaartekracht
```



{{< licentie rel="http://creativecommons.org/licenses/by-nc-sa/4.0/">}}
