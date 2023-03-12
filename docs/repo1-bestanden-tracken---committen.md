### Bestanden tracken & committen

Maak een nieuw bestand hello.txt aan met de tekst "hello world":

	$ echo "hello world" > hello.txt

Voer opnieuw het `git status` commando uit:

	$ git status
	# On branch master
	#
	# No commits yet
	#
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	hello.txt
	nothing added to commit but untracked files present (use "git add" to track)

Git laat ons weten dat er bestanden aanwezig zijn in je directory die nog niet bijgehouden worden door Git (untracked files present). Wanneer je de files wil bijhouden (tracken), dan moet je ze nog adden met het `git add` commando:

	$ git add hello.txt
	$ git status
	# On branch master
	#
	# No commits yet
	#
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	new file:   hello.txt
	#

Nu is git op de hoogte van die file. Dit wil nog niet zeggen dat git automatisch van elke wijziging aan die file een snapshot zal nemen. Je moet zelf beslissen wanneer je een snapshot zal nemen van de wijzigingen in je bestand(en) en deze wil toevoegen aan je git historiek. Dit doe je door een commit uit te voeren:

	$ git commit -m "eerste commit"
	[master (root-commit) 5588c39] eerste commit
	 1 file changed, 1 insertion(+)
	 create mode 100644 hello.txt

`git add` en `git commit` zijn de twee commando's die je heel vaak zal gebruiken tijdens het werken met git.
