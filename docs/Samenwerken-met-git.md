- [Samenwerken met git](#samenwerken-met-git)
  - [Aanmaken \& linken GitHub account](#aanmaken--linken-github-account)
  - [Repository aanmaken \& eerste push](#repository-aanmaken--eerste-push)
  - [Gitignore aanmaken](#gitignore-aanmaken)
  - [Git add - commit - push](#git-add---commit---push)
  - [Bestaande repository binnenhalen](#bestaande-repository-binnenhalen)
  - [push - pull](#push---pull)
  - [rebase](#rebase)
- [Merge conflicts](#merge-conflicts)
- [Git branches](#git-branches)
- [Git Resources](#git-resources)


## Samenwerken met git

Tot nu toe hebben we lokaal gewerkt met git. Je kan ook met meerdere mensen samenwerken aan 1 repository door te werken met een remote server. Iedereen heeft een lokale kopie van de repository staan, en kan zijn wijzigingen via een remote server gaan synchronizeren met andere mensen die de repository hebben staan.

In principe kan je elke computer waarop je de git command tools hebt geïnstalleerd gebruiken als server. Het is dan alleen niet zo praktisch om samen te werken van thuis uit, je moet er dan voor zorgen dat je computer extern bereikbaar is en iedereen die samenwerkt moet dan je ip adres of hostname weten.

Daarom maken we gebruik van een hosted git omgeving. Hier zijn meerdere opties voor, wij zullen gebruik maken van GitHub.

### Aanmaken & linken GitHub account

We zullen eenmalig een GitHub account aanmaken en onze GitHub credentials linken aan onze computer, zodat we niet telkens opnieuw ons wachtwoord moeten ingeven.

Surf naar [https://github.com](https://github.com) en maak een account aan. Ga daarna naar [https://education.github.com/pack](https://education.github.com/pack) en vraag een educational pack aan door te klikken op _Get your pack_, dit zal handig zijn om private repositories aan te maken.

Open daarna een terminal window. We zullen onze naam & email adres koppelen aan git, zodat git weet wie een commit uitvoert. Zorg dat je email adres het adres is dat je gebruikte om je GitHub account aan te maken:

	$ git config --global user.name "Your Name Here"
	$ git config --global user.email "your_email@example.com"

Daarna configureren we git om gebruik te maken van onze OSX keychain om paswoorden op te slaan:

	$ git config --global credential.helper osxkeychain

### Repository aanmaken & eerste push

Login op je GitHub account, en klik op de "New repository" button. Kies een naam voor je repository en klik op de "Create Repository" button.

Open een terminal venster en navigeer via `cd` commandos naar de map van de git repository met de "hello world" files. We zullen er voor zorgen dat we onze lokale repository via GitHub kunnen synchronizeren, door een "remote" te adden. Een remote is een locatie waarmee je een git repository kan synchronizeren:

	$ git remote add origin https://github.com/frederikduchi/dev3-demo.git
	$ git branch -M main
	$ git push -u origin main
	Enumerating objects: 17, done.
	Counting objects: 100% (17/17), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (10/10), done.
	Writing objects: 100% (17/17), 8.98 KiB | 4.49 MiB/s, done.
	Total 17 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), done.
	To https://github.com/frederikduchi/dev3-demo.git
	 * [new branch]      main -> main
	Branch 'main' set up to track remote branch 'main' from 'origin'.

Het `git push` commando zal lokale, niet-gesynchronizeerde wijzigingen uploaden naar de remote lokatie. Het `-u` attribuut gebruik je de allereerste keer, om ervoor te zorgen dat je bij toekomstige synchonizaties de remote name niet meer moet opgeven. Je kan dan in de toekomst gewoon `git push` uitvoeren.

### Gitignore aanmaken

Vergeet niet om meteen al een `.gitignore` bestand aan te maken, met onder andere ignores voor `node_modules`, `.DS_Store` en eventueel `dist`. Zo vermijd je dat deze mappen en bestanden mee gesynchroniseerd worden!

### Git add - commit - push

Vanaf nu kun je commits gaan pushen naar de online repository. Meestal bundel je verschillende lokale commits wanneer je gaat pushen. Dit hebben we in feite reeds gedaan met onze eerste push: alle commits die we eerder uitvoerden, staan nu ook op de online repository.

Wis het `world.txt` bestand, add & commit. We maken gebruik van `git add -u .` om ervoor te zorgen dat de delete actie van die file gestaged wordt:

	$ rm world.txt
	$ git add -u .
	$ git commit -m "removed world file"
	[master 0b0d3b8] removed world file
	 1 file changed, 1 deletion(-)
	 delete mode 100644 world.txt

Maak een README.md bestand aan, met een beetje info over de repository:

	$ echo "Demo repository" > README.md
	$ git add .
	$ git commit -m "added readme file"
	[master a8515e0] added readme file
	 1 file changed, 1 insertion(+)
	 create mode 100644 README.md

Voer een `git status` uit. Je ziet in het status rapport dat de repository 2 commits voorsprong heeft op de online versie:

	# On branch master
	# Your branch is ahead of 'origin/main' by 2 commits.
	# (use "git push" to publish your local commits)
	nothing to commit (working directory clean)

Doe een `git push` om je commits op GitHub te plaatsen:

	Enumerating objects: 6, done.
	Counting objects: 100% (6/6), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (4/4), done.
	Writing objects: 100% (5/5), 488 bytes | 488.00 KiB/s, done.
	Total 5 (delta 2), reused 0 (delta 0)
	remote: Resolving deltas: 100% (2/2), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   f1e8b69..a8515e0  main -> main

Wanneer je de repository via je browser bekijkt, zal je zien dat de inhoud van de `README.md` file, getoond wordt onder de lijst van files. Dit is een bestand in het Markdown formaat. Markdown is een eenvoudige markup taal om documenten op te maken. Meer informatie hierover kan je onder andere vinden op wikipedia: [http://en.wikipedia.org/wiki/Markdown](http://en.wikipedia.org/wiki/Markdown).

### Bestaande repository binnenhalen

Eens een repository aangemaakt is, en op een server zoals GitHub staat, kun je hem ook op andere computers / locaties binnenhalen. De repository een eerste keer binnenhalen doe je via het `git clone` commando. Vanaf dan kun je updates binnenhalen via het `git pull` commando. `git pull` is het omgekeerde van `git push`, en zal je gebruiken om updates die je nog niet lokaal hebt staan binnen te halen.

Open een tweede terminal venster, navigeer naar de bovenliggende map van je originele git repository en maak een map aan waarin je een duplicaat van de repository zal clonen:

	$ mkdir project2
	$ cd project2

Voer het git clone commando uit, om de online repository binnen te halen (wijzig wel de url naar die van je eigen repository:

	$ git clone https://github.com/frederikduchi/dev3-demo
	Cloning into 'dev3-demo'...
	remote: Enumerating objects: 22, done.
	remote: Counting objects: 100% (22/22), done.
	remote: Compressing objects: 100% (11/11), done.
	remote: Total 22 (delta 3), reused 22 (delta 3), pack-reused 0
	Unpacking objects: 100% (22/22), done.

Je hebt nu 2 clones van dezelfde repository op je computer. Eentje in de map project en eentje in de map project2. We zullen deze twee gebruiken om synchronisaties en merges te testen.

### push - pull

We simuleren samenwerken met 2 users door op in twee verschillende mappen met dezelfde remote (online repository) te synchronizeren. Let bij de volgende acties op in welke map je de nodige commando's uitvoert (de project map staat vanaf nu telkens voor het dollarteken in het uit te voeren commando).

In map 1 maken we een nieuw bestand `project.txt` aan, we adden, committen en pushen naar de remote:

	project$ echo "created in project" > project.txt
	project$ git add .
	project$ git commit -m "added project.txt file"
	[main 3dc1c52] add project.txt file
	 1 file changed, 1 insertion(+)
	 create mode 100644 project.txt
	 
	project$ git push
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 300 bytes | 300.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   a8515e0..3dc1c52  main -> main

In map 2 (dev3-demo) maken we een nieuw bestand `project2.txt` aan, doen we een add & commit en proberen we te pushen naar de remote:

	project2$ echo "created in project2" > project2.txt
	project2$ git add .
	project2$ git commit -m "added project2.txt file"
	[master 3bdfe55] added project2.txt file
	 1 file changed, 1 insertion(+)
	 create mode 100644 project2.txt
	project2$ git push
	To https://github.com/frederikduchi/dev3-demo
	 ! [rejected]        main -> main (fetch first)
	error: failed to push some refs to 'https://github.com/frederikduchi/dev3-demo'
	hint: Updates were rejected because the remote contains work that you do
	hint: not have locally. This is usually caused by another repository pushing
	hint: to the same ref. You may want to first integrate the remote changes
	hint: (e.g., 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.


We krijgen een fout: er zijn nieuwe commits op de remote, die we nog niet hebben binnengehaald in onze project2 clone. We moeten deze eerst pullen, voor we een push kunnen doen:

	project2$ git pull

We krijgen een vim of nano editor te zien om een merge uit te voeren. Je kan hier een custom message ingeven. Geef `:quit` in om de vim editor te sluiten en verder te doen met de merge.

	remote: Enumerating objects: 4, done.
	remote: Counting objects: 100% (4/4), done.
	remote: Compressing objects: 100% (1/1), done.
	remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	From https://github.com/frederikduchi/dev3-demo
	   a8515e0..3dc1c52  main       -> origin/main
	Merge made by the 'recursive' strategy.
	 project.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 project.txt

Wanneer je een `git status` uitvoert, zal je zien dat je 2 commits voor bent op de remote: 1 commit is de merge commit, en een tweede commit is de `project2.txt` commit:

	project2$ git status
	# On branch main
	# Your branch is ahead of 'origin/main' by 2 commits.
	#
	nothing to commit (working directory clean)

Doe opnieuw een push van die commits naar de remote. Het pushen lukt deze keer wel:

	project2$ git push
	Enumerating objects: 7, done.
	Counting objects: 100% (7/7), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (4/4), done.
	Writing objects: 100% (5/5), 551 bytes | 551.00 KiB/s, done.
	Total 5 (delta 2), reused 0 (delta 0)
	remote: Resolving deltas: 100% (2/2), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo
	   3dc1c52..c18628a  main -> main


Haal nu deze commits ook op in je eerste map (niet vergeten van map te wisselen dus) via een `git pull` commando:

	project$ git pull
	remote: Enumerating objects: 7, done.
	remote: Counting objects: 100% (7/7), done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 5 (delta 2), reused 5 (delta 2), pack-reused 0
	Unpacking objects: 100% (5/5), done.
	From https://github.com/frederikduchi/dev3-demo
	   3dc1c52..c18628a  main       -> origin/main
	Updating 3dc1c52..c18628a
	Fast-forward
	 project2.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 project2.txt

### rebase

Wij zullen voorlopig werken met een centralized workflow: we werken met meerdere mensen samen op 1 master branch via 1 remote. Er zijn nog andere, meer geavanceerde workflows die werken via branches en forks. Deze zijn echter al iets complexer.

In het voorgaande scenario hebben we een merge commit toegevoegd om een niet up-to-date repository te fast-forwarden. Deze is bij een centralized workflow overbodig: we kunnen beter gebruik maken van een rebase bij de `git pull`. Een rebase zal eerst alle commits van de remote uitvoeren, en jouw commits erachter uitvoeren, in plaats van standaard een merge commit uit te voeren.

Doe een delete van `project.txt` in de project map:

	project$ rm project.txt
	project$ git add -u .
	project$ git commit -m "removed project.txt"
	[main de80b79] removed project.txt
	 1 file changed, 1 deletion(-)
	 delete mode 100644 project.txt
	project$ git push
	Enumerating objects: 3, done.
	Counting objects: 100% (3/3), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (2/2), 233 bytes | 233.00 KiB/s, done.
	Total 2 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   c18628a..de80b79  main -> main

Doe daarna een delete van `project2.txt` in de `project2` map. We zullen ook hier eerst een pull moeten doen voordat we kunnen pushen. Het verschil bij de pull is dat we een rebase flag meegeven, om ervoor te zorgen dat eerst alle commits van de remote repository uitgevoerd worden, en daarna onze eigen commits:

	project2$ rm project2.txt
	project2$ git add -u .
	project2$ git commit -m "removed project2.txt"
	[main 6be65fb] removed project2.txt
	 1 file changed, 1 deletion(-)
	 delete mode 100644 project2.txt
	 
	project2$ git pull --rebase
	remote: Enumerating objects: 3, done.
	remote: Counting objects: 100% (3/3), done.
	remote: Compressing objects: 100% (1/1), done.
	remote: Total 2 (delta 1), reused 2 (delta 1), pack-reused 0
	Unpacking objects: 100% (2/2), done.
	From https://github.com/frederikduchi/dev3-demo
	   c18628a..de80b79  main       -> origin/main
	First, rewinding head to replay your work on top of it...
	Applying: removed project2.txt


Op deze manier wordt er geen merge commit aangemaakt. Wanneer je een `git status` uitvoert, zie je dat je nu maar 1 commit voorsprong hebt op de remote repository, in plaats van 2:

	project2$ git status
	# On branch main
	# Your branch is ahead of 'origin/main' by 1 commit.
	  (use "git push" to publish your local commits)
	#
	nothing to commit (working directory clean)

Push naar de remote repository. Doe ook opnieuw een pull in de project map, zodat beide repositories up-to-date zijn.

## Merge conflicts

Tot nu toe hebben we braafjes in aparte files wijzigingen aangebracht. Het kan echter gebeuren dat je met 2 personen in dezelfde file wijzigingen hebt aangebracht, en dat er een conflict optreedt.

Pas in de `project` map de tekst aan in `hello.txt` en push deze naar de remote repository:

	project$ echo "edit in project" > hello.txt
	project$ git add .
	project$ git commit -m "changed hello.txt"
	[main f1c4e08] changed hello.txt
	 1 file changed, 1 insertion(+), 1 deletion(-)
	 
	project$ git push
	Enumerating objects: 5, done.
	Counting objects: 100% (5/5), done.
	Delta compression using up to 12 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 284 bytes | 284.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/frederikduchi/dev3-demo.git
	   8f2400d..f1c4e08  main -> main

Pas nu ook in de `project2` map de tekst in dezelfde file aan en probeer te pushen:

	project2$ echo "edit in project2" > hello.txt
	project2$ git add .
	project2$ git commit -m "changed hello.txt in project2"
	[main 45b7ea9] chenged hello.txt in project2
	 1 file changed, 1 insertion(+), 1 deletion(-)
	 
	project2$ git push
	To https://github.com/frederikduchi/dev3-demo
	 ! [rejected]        main -> main (fetch first)
	error: failed to push some refs to 'https://github.com/frederikduchi/dev3-demo'
	hint: Updates were rejected because the remote contains work that you do
	hint: not have locally. This is usually caused by another repository pushing
	hint: to the same ref. You may want to first integrate the remote changes
	hint: (e.g., 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.

We moeten eerst nog pullen, voor we kunnen pushen:

	project2$ git pull --rebase
	remote: Enumerating objects: 5, done.
	remote: Counting objects: 100% (5/5), done.
	remote: Compressing objects: 100% (1/1), done.
	remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	From https://github.com/frederikduchi/dev3-demo
	   8f2400d..f1c4e08  main       -> origin/main
	First, rewinding head to replay your work on top of it...
	Applying: chenged hello.txt in project2
	Using index info to reconstruct a base tree...
	M	hello.txt
	Falling back to patching base and 3-way merge...
	Auto-merging hello.txt
	CONFLICT (content): Merge conflict in hello.txt
	error: Failed to merge in the changes.
	Patch failed at 0001 chenged hello.txt in project2
	hint: Use 'git am --show-current-patch' to see the failed patch
	Resolve all conflicts manually, mark them as resolved with
	"git add/rm <conflicted_files>", then run "git rebase --continue".
	You can instead skip this commit: run "git rebase --skip".
	To abort and get back to the state before "git rebase", run "git rebase --abort".


We krijgen een merge conflict, doordat we in beide repositories dezelfde file wijzigden. We moeten eerst dit conflict oplossen, voor dat de rebase kan verderdoen.

Via `git status` kun je een lijst opvragen met de merge conflicts:

	project2$ git status
	#rebase in progress; onto f1c4e08
	#You are currently rebasing branch 'main' on 'f1c4e08'.
	#  (fix conflicts and then run "git rebase --continue")
	#  (use "git rebase --skip" to skip this patch)
	#  (use "git rebase --abort" to check out the original branch)
	#
	#Unmerged paths:
	#  (use "git restore --staged <file>..." to unstage)
	#  (use "git add <file>..." to mark resolution)
	#	both modified:   hello.txt
	no changes added to commit (use "git add" and/or "git commit -a")

Je krijgt de melding dat je aan het rebasen bent. Bij "Unmerged paths" zie je de files die in conflict zijn. Je moet eerste het conflict oplossen, door de file te editen, voor je kan verder doen met de rebase.

Open het txt bestand in een teksteditor. Je zal zien dat zowel de content uit `project` als `project2` aanwezig is:

	<<<<<<< HEAD
	edit in project
	=======
	edit in project2
	>>>>>>> changed hello.txt in project2

Pas de tekst aan naar:

	edit in project
	and edit in project2

Add deze aan de rebase actie en continue:

	project2$ git add hello.txt
	project2$ git rebase --continue
	Applying: changed hello.txt in project2

Wanneer je nu een git status uitvoert, zal je zien dat je opnieuw op de master / main branch zit, en 1 commit voorsprong hebt op de remote:

	project2$ git status
	# On branch main
	# Your branch is ahead of 'origin/main' by 1 commit.
	#
	nothing to commit (working directory clean)

Nu kan je opnieuw pushen naar de remote:

	project2$ git push
	Counting objects: 5, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 326 bytes, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To https://github.com/devinekask/git-demo
	   7f3b200..920c81f  master -> master

Doe een `git pull` in de andere map, zodat beide mappen terug in sync zijn.


## Git branches
Via Git kan je ook gebruik maken van branches.

Je kan branches toevoegen om:
- Nieuwe features te ontwikkelen
- Bugs te fixen
- Te experimenteren met nieuwe ideeën zonder je production code (code die online staat) te beïnvloeden

Dit is een walkthrough om te werken met 2 branches, namelijk `develop` en `master` branches. Op de `master` branch kan je de production ready code terugvinden. Op de `develop` branch daarentegen kan je code pushen die nog niet volledig klaar is om aan je eindgebruiker te tonen.

Vanaf het moment dat je tevreden bent met de (bugvrije) code in de `develop` branch, kan je deze "mergen" naar de `master` branch. Dit proces wordt verder uitgelegd.

Je werkt verder op het huidige project.

Maak dan een branch `develop` aan door het volgende commando uit te voeren:

	$ git branch develop

Een overzicht van je branches kun je opvragen via deze commando:

	$ git branch

Nu we een nieuwe `develop` branch hebben aangemaakt, kunnen we ernaar switchen door `git checkout develop` uit te voeren:

	$ git checkout develop

Push deze `develop` branch naar remote en bekijk het resultaat op GitHub:

	$ git push origin develop

Doe enkele commits op de `develop` branch. Je kan deze tussendoor gerust pushen naar Github (via `git push origin develop`).

We zouden nu graag onze code van `develop` mergen met onze `master` code, zodat beide branches dezelfde code bevatten (nu heeft `develop` namelijk meer commits dan `master`, oftewel `develop` staat voor op `master` - bekijk dit verschil ook eens in Github). Hiervoor moeten we eerst terugswitchen naar onze `master` branch om in een volgende stap `develop` erin te mergen:

	$ git checkout main

De merge van `develop` in `master` kan via een `git merge` commando:

	$ git merge develop main

Switch onmiddellijk terug naar `develop`, zodat je niet per ongeluk zit te ontwikkelen in de `master` branch (we willen dat onze `develop` branch altijd de meest recente code bevat):

	$ git checkout develop

Push de branches:

	$ git push origin main
	$ git push origin develop

Als alternatief kan je ze ook allemaal in één keer pushen:

	$ git push --all origin

Op een andere locatie kun je dan de branches pullen (binnentrekken):

	$ git pull --rebase origin develop
	$ git pull --rebase origin main

## Git Resources

Dit is een basis introductie om je op weg te helpen met git. Er is nog heel wat meer mogelijk met git & github. Meer informatie & tutorials kun je onder andere vinden op volgende locaties:

* [https://www.atlassian.com/git/](https://www.atlassian.com/git/)
* [https://help.github.com/](https://help.github.com/)
* [http://git-scm.com/book](http://git-scm.com/book)
