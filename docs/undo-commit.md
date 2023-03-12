### Commits ongedaan maken

Stel: je hebt bepaalde wijzigingen gecommit, maar om een of andere reden wil je die ongedaan maken.

	$ echo "hello devine" > hello.txt
	$ git add hello.txt
	$ git commit -m "changed, but not sure about it"

Je kan 2 dingen doen: ofwel een nieuwe commit maken die de wijzigingen uit de vorige commit ongedaan maakt (`git revert HEAD`), ofwel de commit volledig uit de historiek gaan wissen (`git reset --hard referentie-naar-commit`).

	$ git revert HEAD

Je terminal zal nu een vim of nano editor tonen, waarin je een commit message kan typen. Pas eventueel de default message aan, en typ in vim `:quit` wanneer je klaar bent. Voor nano gebruik je Ctrl + X, gevolgd door Yes.

	[master 2bc740f] Revert "changed, but not sure about it"
	 1 file changed, 1 insertion(+), 1 deletion(-)

De file zal nu de inhoud bevatten van voor de laatste commit.

Je kan ook een andere editor instellen voor de merge message edits. In plaats van vim is nano een gebruiksvriendelijker alternatief:

```bash
git config --global core.editor "nano"
```

Je kan trouwens de commit historiek van een repository bekijken via het `git log` commando:

	$ git log
	commit 2bc740f2af93348267c6b3558e1037c5db540600 (HEAD -> master)
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:57:33 2021 +0200

	    Revert "changed, but not sure about it"

	    This reverts commit 8d977cb2d4855a782e261015645e017c1e128000.

	commit 8d977cb2d4855a782e261015645e017c1e128000
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:56:55 2021 +0200

	    changed, but not sure about it

	commit 5aa411822d8546ef1cd73addc20a022a74deae91
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:54:26 2021 +0200

	    changed, but not sure about it

	commit 9720321677e0798b540b287398edeaadcb630b17
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:35:21 2021 +0200

	    welcome dev3 + new world file

	commit 7f65053ee86593fb29a3102e03f7ae3f44b112d7
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:32:22 2021 +0200

	    world gewijzigd naar devine

	commit 5588c399cd15bc841c89158d72cc4d3938581196
	Author: Frederik Duchi <frederik.duchi@howest.be>
	Date:   Wed Sep 1 09:30:22 2021 +0200

	    eerste commit


Je ziet dat de "foute" commit nog steeds in de git historiek aanwezig is, en dat de wijzigingen via een nieuwe commit ongedaan gemaakt werden. Merk ook op dat elke commit een unieke SHA1-hash id heeft. Deze ids kun je gebruiken om commits te specifiëren bij bepaalde commano's.

Een meer drastische manier om commits ongedaan te maken, is via het `git reset` commando. Via git reset ga je je working tree gaan resetten naar een bepaalde commit en alle commits na die commit wissen uit de repository.

We willen terug naar de status gaan van onze commit "welcome dev3 + new world file". Via git log, komen we te weten dat het SHA1 id `9720321677e0798b540b287398edeaadcb630b17` is. Specifieer het SHA1 id van de commit naar waar je wil resetten na het commando. Je hoeft niet het ganse id te specifiëren: de eerste 4 karakters zijn vaak voldoende (ten minste als deze uniek zijn):

	$ git reset --hard 9720
	HEAD is now at 9720321 welcome dev3 + new world file

Wanneer je nu opnieuw git log uitvoert, zie je dat de commits na 9720 verdwenen zijn:

	$ git log
	commit 9720321677e0798b540b287398edeaadcb630b17 (HEAD -> master)
	Author: Frederik Duchi <frederik.duchi@telenet.be>
	Date:   Wed Sep 1 09:35:21 2021 +0200

	    welcome dev3 + new world file

	commit 7f65053ee86593fb29a3102e03f7ae3f44b112d7
	Author: Frederik Duchi <frederik.duchi@telenet.be>
	Date:   Wed Sep 1 09:32:22 2021 +0200

	    world gewijzigd naar devine

	commit 5588c399cd15bc841c89158d72cc4d3938581196
	Author: Frederik Duchi <frederik.duchi@telenet.be>
	Date:   Wed Sep 1 09:30:22 2021 +0200

	    eerste commit

Zo'n `git reset` commando ga je enkel gebruiken om lokale commits ongedaan te maken. Eens je samenwerkt met anderen, en commits reeds verspreid zijn onder andere users, dan gebruik je het `git revert` commando om een nieuwe commit te maken die een vorige commit ongedaan maakt.
