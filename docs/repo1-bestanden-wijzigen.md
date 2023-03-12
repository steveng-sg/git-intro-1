### Bestanden wijzigen

Pas de inhoud van het bestand aan naar "hello devine", en voer het git status commando uit:

	$ echo "hello devine" > hello.txt
	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Git heeft gedetecteerd dat er wijzigingen zijn gebeurd aan een reeds getracked bestand. Je zal deze opnieuw moeten "adden", om deze wijzigingen in de wachtrij te zetten voor een commit (wordt stage for commit genoemd):

	$ git add hello.txt

Commit vervolgens deze wijzigingen:

	$ git commit -m "world gewijzigd naar devine"
	[master 7f65053] world gewijzigd naar devine
	 1 file changed, 1 insertion(+), 1 deletion(-)

Je kan natuurlijk ook meerdere wijzigingen in 1x adden en committen. Pas de tekst aan, en maak een tweede file aan:

	$ echo "hello development 3" > hello.txt
	$ echo "hello" > world.txt

Git status zal nu 2 zaken rapporteren: het wijzigen van een reeds getrackte file, en het detecteren van een nieuwe file die nog niet getracked wordt:

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git restore <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	world.txt
	no changes added to commit (use "git add" and/or "git commit -a")

Je kan nu deze twee zaken afzonderlijk stagen door 2x een git add uit te voeren, maar dit kan ook in 1 keer, door `git add .`

	$ git add .
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	modified:   hello.txt
	#	new file:   world.txt
	#

Nu zijn beide gestaged voor commit, en kan je met 1 commit ze loggen in de git repository:

	$ git commit -m "welcome dev3 + new world file"
	 [master 9720321] welcome dev3 + new world file
	 2 files changed, 2 insertions(+), 1 deletion(-)
	 create mode 100644 world.txt