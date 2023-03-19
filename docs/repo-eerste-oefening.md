# Een eerste oefening
## CLI basis

* maak een nieuwe directory, onder de map /gh, met als naam datumgen
* open deze map met vs code
* maak een nieuw bestand datum.py
  * dit is een python bestandje. Het bestand vraagt eerst je naam, en zegt je dan goeiedag, en geeft de datum en het uur van vandaag. Kopieer en plak volgende code in het bestand:
```python
import datetime

name = input("Wat is je naam? ")
now = datetime.datetime.now()

print("Hallo {name}, het is nu {now.strftime('%H:%M:%S')} op {now.strftime('%d-%m-%Y')}.")
```
### README.md
* Maak een nieuw bestand README.md
    * Elke github repo bevat een README.md bestand, waar een korte inleiding gegeven wordt over de repo.
    * een .md bestand is een markdown bestand. Het wordt gebruikt om op eenvoudige wijze een layout te verkrijgen in een teksbestand. Deze volledige website is opgesteld in markdown.
    * De syntax is eenvoudig. Je kan een voorbeeld vinden op deze pagina.
    * in vs code zoek en installeer je de extensie "Markdown preview enhanced".
    * In je .md-bestand klik je met je rechtermuisknop, en selecteer "Markdown Preview Enhanced: open preview to the side"

```
# Koppen
De # maakt een koptekst. # = kop 1, ## = kop 2, etc.

* List item
Een * met een spatie maakt een genummerde lijst. Een tab met een * doet de lijst inspringen. 

*cursief*
dit maakt de tekst tussen de * cursief

**vet**
dit maakt de tekst tussen de ** vet.

- [ ] Checklist
Een - gevolgd door spatie en [ ] maakt een checklist. Handig voor issues.
```
* Plak volgende tekst in je README.md bestand, en zorg dat deze een goede layout heeft met markdown-syntax.
```
Een datumgenerator

In deze repository vind je de code om een moderne datumgenerator te maken. Deze heeft volgende eigenschappen:
Start op van de command line
Persoonlijke begroeting
is zeer snel

Opbouw van deze repo
Alle bestanden staan onder de hoofdmap. Er zijn geen submappen.

Samenwerking
Indien je graag wilt helpen dit interessant programma te ontwikkelen, stuur een bericht naar de eigenaar van deze repo.


```


