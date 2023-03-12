### Wijzigingen vóór staging ongedaan maken

Pas de tekst in hello.txt opnieuw aan naar "hello devine", maar add deze nog niet:

	$ echo "hello devine" > hello.txt

Voer een git status uit, git heeft changes gedetecteerd die nog niet staged for commit zijn:

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Je krijgt hier al een hint hoe je de wijzigingen in je working directory kunt ongedaan maken: via het git restore commando. Voer dit commando uit, en controleer de status van de repository:

	$ git restore hello.txt
	$ git status
	# On branch master
	nothing to commit (working directory clean)

De wijzigingen aan hello.txt zijn ongedaan gemaakt. Als je de inhoud van de file bekijkt via het cat commando, zul je zien dat deze de inhoud bevat van je laatste commit:

	$ cat hello.txt
	hello development 3