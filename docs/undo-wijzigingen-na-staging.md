### Wijzigingen na staging ongedaan maken

Pas de tekst opnieuw aan naar "hello devine", stage deze wijzigingen via het add commando, maar commit deze nog niet:

	$ echo "hello devine" > hello.txt
	$ git add hello.txt
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	modified:   hello.txt
	#

Je krijgt een hint hoe je deze wijzigingen kunt unstagen: via git restore --staged:

	$ git restore --staged hello.txt

De file is nog steeds gewijzigd, maar de wijzigingen zijn niet meer gestaged:

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Je kunt deze nu definitief ongedaan maken, door - net zoals in voorgaande topic - git restore te gebruiken:

	$ git restore hello.txt