### Aanmaken van een nieuwe git-repository

Je kan van elke bestaande map een git repository maken met het `git init` commando. Het maakt niet uit of hier al bestanden of submappen in aanwezig zijn. Wij zullen starten met een nieuwe lege map, maar weet dat dit niet nodig is om een project via git te beheren.

Maak een nieuwe map aan en maak hiervan een git repository (opmerking: de dollartekens duiden erop dat dit over een command line input gaat door de gebruiker, en typ je niet):

	$ mkdir project
	$ cd project
	$ git init
	Initialized empty Git repository in /Users/frederikduchi/Documents/development3/project/.git/

Het `git init` commando zal een verborgen map  met de naam .git aanmaken. Hierin zit alle informatie over de repository & z'n historiek.

Via het `git status` commando kun je wat meer informatie opvragen over de huidige status van de repository. Dit gebruik je vaak om te zien welke bestanden er gewijzigd zijn, of er nieuwe bestanden zijn, of er bestanden gewist zijn.

	$ git status
	# On branch master
	#
	# No commits yet
	#
	nothing to commit (create/copy files and use "git add" to track)