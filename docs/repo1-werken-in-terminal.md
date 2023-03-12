### Werken in Terminal

Vooraleer we git specifieke commandos gaan gebruiken, zullen we even een korte opfrissing doen van enkele belangrijke Terminal commando's. Volgende commando's zou elke developer vlot moeten kunnen gebruiken:

* `ls`: Toon een lijst van bestanden en mappen in de actieve map. Indien je ook de verborgen bestanden & de bestandsattributen wil zien, kun je `ls -al` uitvoeren.
* `cd naamvanmap`: Hiermee navigeer je naar de map met de naam die na het commando staat. Deze map wordt dan de actieve map in je Terminal. In dit voorbeeld navigeer je naar de map met de naam "naamvanmap". In plaats van een relatieve naam (dus een naam van een map die in de huidige actieve map staat), kun je ook een volledig pad invullen (beginnen met een forward slash). Tip: je kan vanuit je finder een map of bestand slepen naar het terminal venster om het volledige pad naar die map of bestand te plaatsen in het venster.
* `cd ..`: Navigeer naar de bovenliggende map, zodat deze de actieve map wordt.
* `mkdir naamvanmap`: maak een map aan met de naam gespecifieerd na het commando. In dit geval maak je een map aan met de naam "naamvanmap" in de actieve map.
* `rm -d naamvanmap`: wis een bepaalde map. Dit lukt enkel als de map leeg is. Wanneer je een niet-lege map wil wissen, dan kun je extra opties gebruiken: `rm -rdf naamvanmap` zal de map inclusief submappen en files wissen.
* `rm naamvanbestand`: wis een bepaald bestand.
* `mv origineleneem nieuwenaam`: verplaats of hernoem een bestand. Je kan ook absolute / relatieve paden gebruiken om bestanden te verplaatsen naar een andere map.
* `cp originelenaam nieuwenaam`: kopieer een bestand naar een nieuwe locatie.
* `cat naamvanbestand`: toon de inhoud van een bepaald bestand in je terminal venster.
* `echo "hello world"`: toon de tekst tussen de quotes in het terminal venster.

Door gebruik te maken van de `tab`-toets, kun je autocomplete triggeren op commando's of bestands en mapnamen. Typ een deel van het commando of een deel van het pad en druk op tab om automatisch aan te vullen. Zo kun je heel wat tijd besparen, en vermijd je bovendien typfouten.

Je kan ook output van een commando wegschrijven naar een bestand, door gebruik te maken van het `>` karakter:

* `ls > test.txt` zal de output van het ls commando wegschrijven in een bestand met de naam test.txt.
* `echo "hello world" > hello.txt` zal de output van het echo commando (de tekst "hello world") wegschrijven in een bestand met de naam hello.txt.

Dit zijn enkele basiscommando's die je als je broekzak moet kennen. Dit is niets git-specifiek! Je zal deze commando's ook gebruiken wanneer je aan de slag gaat met Node.js en module bundlers zoals Gulp, Webpack of ViteJS.