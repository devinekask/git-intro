- [Git](#git)
  * [About Git](#over-git)
  * [Internal operation](#interne-werking)
  * [A first repository](#een-eerste-repository)
    + [Working in Terminal](#werken-in-terminal)
    + [Create a new git-repository](#aanmaken-van-een-nieuwe-git-repository)
    + [Track & commit files](#bestanden-tracken---committen)
    + [Modify files](#bestanden-wijzigen)
    + [git add -A .](#git-add--a-)
  * [Undo changes](#wijzigingen-ongedaan-maken)
    + [Undo changes before staging](#wijzigingen-v--r-staging-ongedaan-maken)
    + [Undo changes after staging](#wijzigingen-na-staging-ongedaan-maken)
    + [Undo commits](#commits-ongedaan-maken)
  * [Ignore files](#bestanden-negeren)
    + [Delete files](#bestanden-wissen)
    + [Delete files & folders from the commit history](#bestanden---mappen-verwijderen-uit-je-volledige-historiek)
    + [.gitignore](#gitignore)
  * [Collaboration with git](#samenwerken-met-git)
    + [Create & link GitHub account](#aanmaken---linken-github-account)
    + [Create repository & first push](#repository-aanmaken---eerste-push)
    + [Create gitignore](#gitignore-aanmaken)
    + [Git add - commit - push](#git-add---commit---push)
    + [Pull existing repository](#bestaande-repository-binnenhalen)
    + [push - pull](#push---pull)
    + [rebase](#rebase)
  * [Merge conflicts](#merge-conflicts)
  * [Git branches](#git-branches)
  * [Git Resources](#git-resources)



# Git #
## About Git ##
Git is a version control system. It allows you to collaborate on projects with several people and to keep a history of the project.

It was launched in April 2005 by Linus Torvalds - the father of Linux. Code management systems were nothing new, some important systems in the past were:

* SCSS early 1970s
* RCS early 80s
* CVS was launched in 1986
* SVN in 2001

Linux development was done in the early years with Bitkeeper VCS. However, in 2005 Bitkeeper imposed some additional restrictions on the free open source version, so that Linux could no longer be developed via this system. Linus looked for alternatives, but found none that met his requirements:

* Easy to do distributed development
* Being scalable: being able to collaborate with 1000+ developers
* Being Fast & Efficient and Reliable
* Know who did what
* Transaction support: bundle multiple actions
* Branching support: branches of the project that can be merged back into the main project.
* Distributed repositories: project with history is not kept centrally.
* For free

When he couldn't find an alternative that met these requirements, he decided to develop his own system: GIT was born.

The name GIT is not an abbreviation, but a reference to Linus himself: it is slang for "an unpleasant person". Like Linux, he wanted a name that refers to himself. Afterwards, the community put the abbreviation "Global Information Tracker" on it.

## Internal Operation ##

Your files are stored in a repository. This repository contains information about the contents of the files, their name, location and history.

* the contents of files are stored in blob objects
* history is kept in commit objects
* the structure is maintained in tree objects

If you have multiple files with the same content, the tree will reference the same blob object multiple times, saving storage.

## A first repository

We will use git from the command line. There are some applications that allow you to execute git commands via a GUI, but if you want to perform more advanced actions you will have to go back to the command line anyway.

Git is installed when you install the xcode command line tools. So if you have already done this (for example to make Node.js work), you can get started right away. Another option (without the command line tools) is to download and install git from [http://git-scm.com/downloads](http://git-scm.com/downloads).

### Working in Terminal

Before we start using git specific commands, let's do a quick refresher on some important Terminal commands. The following commands should be easy for any developer to use:

* `ls`: Display a list of files and folders in the current folder. If you also want to see the hidden files & the file attributes, you can run `ls -al`.
* `cd foldername`: Navigates to the folder named after the command. This folder will then become the active folder in your Terminal. In this example, navigate to the folder named "foldername". Instead of a relative name (ie a name of a folder that is in the current active folder), you can also enter a full path (starting with a forward slash). Tip: you can drag a folder or file from your finder to the terminal window to place the full path to that folder or file in the window.
* `cd ..`: Navigate to the parent directory so that it becomes the active directory.
* `mkdir foldername`: create a folder with the name specified after the command. In this case, create a folder called "foldername" in the active folder.
* `rm -d foldername`: delete a particular folder. This only works if the folder is empty. If you want to delete a non-empty folder, you can use additional options: `rm -rdf foldername` will delete the folder including subfolders and files.
* `rm filename`: delete a specific file.
* `mv originalname newname`: move or rename a file. You can also use absolute / relative paths to move files to another folder.
* `cp originalname newname`: copy a file to a new location.
* `cat filename`: display the contents of a particular file in your terminal window.
* `echo "hello world"`: display the text between the quotes in the terminal window.

By using the `tab` key, you can trigger autocomplete on commands or file and folder names. Type part of the command or part of the path and press tab to autocomplete. This way you can save a lot of time, and you also avoid typing errors.

You can also write output from a command to a file, using the `>` character:

* `ls > test.txt` will write the output of the ls command to a file called test.txt.
* `echo "hello world" > hello.txt` will write the output of the echo command (the text "hello world") to a file called hello.txt.

These are some basic commands you should know by head. This is nothing git specific! You will also use these commands when getting started with Node.js and module bundlers like Gulp, Webpack or ViteJS.

### Create a new git-repository

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
	#   (use "git rm --cached <file>..." to unstage)
	#
	#	new file:   hello.txt
	#

Nu is git op de hoogte van die file. Dit wil nog niet zeggen dat git automatisch van elke wijziging aan die file een snapshot zal nemen. Je moet zelf beslissen wanneer je een snapshot zal nemen van de wijzigingen in je bestand(en) en deze wil toevoegen aan je git historiek. Dit doe je door een commit uit te voeren:

	$ git commit -m "eerste commit"
	[master (root-commit) 5588c39] eerste commit
	 1 file changed, 1 insertion(+)
	 create mode 100644 hello.txt

`git add` en `git commit` zijn de twee commando's die je heel vaak zal gebruiken tijdens het werken met git.

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

### git add -A . ###

We hebben al eerder gezien dat je met `git add .` alle wijzigingen kunt stagen voor commit. Nu is het zo dat deletes (wissen van files) niet mee gestaged worden. Daarvoor moet je nog de flag -A toevoegen aan het commando.

## Wijzigingen ongedaan maken

Er zijn een 3-tal scenario's wanneer je misschien wijzigingen wil ongedaan maken:

1. Wanneer je wijzigingen hebt aangebracht, maar nog niet ge-add hebt.
2. Wanneer wijzigingen ge-add zijn, maar nog niet gecommit
3. Wanneer je na een commit wil terugkeren naar een vroegere versie.

In elk van deze scenario's kun je wijzigingen ongedaan maken door de juiste git commando's te gebruiken.

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
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Je kunt deze nu definitief ongedaan maken, door - net zoals in voorgaande topic - git checkout te gebruiken:

	$ git restore hello.txt

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

## Bestanden negeren
Het zal niet nodig zijn om alle bestanden in een projectmap bij te houden via Git. Zo is het bijvoorbeeld geen goed idee om een `node_modules` map te tracken in je repository. Ook verborgen systeembestanden, zoals `.DS_Store` hebben geen enkel nut in een repository.

Initialiseer je map als een node project, en koppel bijvoorbeeld webpack aan dit project:

```bash
$ npm init -y
$ npm install webpack --dev
```

We zullen nu "per ongeluk" `node_modules` committen, en kijken om dit nadien recht te zetten.

```bash
$ git add .
$ git commit -m "initial project"
[master 0ead6d0] initial project
 2435 files changed, 385719 insertions(+)
 create mode 120000 node_modules/.bin/acorn
 create mode 120000 node_modules/.bin/browserslist
 create mode 120000 node_modules/.bin/terser
 ...
 create mode 100644 node_modules/yocto-queue/license
 create mode 100644 node_modules/yocto-queue/package.json
 create mode 100644 node_modules/yocto-queue/readme.md
 create mode 100644 package-lock.json
 create mode 100644 package.json

 ```

### Bestanden wissen

Je hebt nu het volledige project, inclusief de `node_modules` toegevoegd aan je git repository.

Dit is overkill, het is niet nodig om de volledige dependency tree mee op te slaan in je git repository. We zullen deze fout nu rechtzetten:

	$ git rm -r --cached node_modules/
	rm 'node_modules/.bin/acorn'
	rm 'node_modules/.bin/browserslist'
	rm 'node_modules/.bin/terser'
	rm 'node_modules/.bin/webpack'
	rm 'node_modules/@types/eslint-scope/LICENSE'
	rm 'node_modules/@types/eslint-scope/README.md'

	...

De --cached optie zorgt ervoor dat de file gewist word uit de repository index, maar wel blijft staan in jouw filesysteem.

Een git status geeft nu het volgende resultaat:

	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git restore --staged <file>..." to unstage)
	#
	#	deleted:    node_modules/.bin/acorn
	#	deleted:    node_modules/.bin/browserslist
	#	deleted:    node_modules/.bin/terser
	#	deleted:    node_modules/.bin/webpack
	#	deleted:    node_modules/@types/eslint-scope/LICENSE
	#	deleted:    node_modules/@types/eslint-scope/README.md
	...

Add & commit nu deze deletes, door de flag -A te gebruiken bij je add:

	$ git add -A .
	$ git commit -m "removed node_modules folder"
	On branch master
	nothing to commit, working tree clean

### Bestanden & mappen verwijderen uit je volledige historiek

We hebben zopas een commit aangemaakt, waarin deze `node_modules` opnieuw verwijderd worden. Er is echter nog steeds een commit waarin deze `node_modules` wél aanwezig zijn, wat onze repository onnodig groot maakt. Indien je mappen of bestanden wil verwijderen uit de volledige historiek van je project, dan moet je nog een stap verder gaan.

Via het git `filter-branch` commando kun je de git historiek aanpassen. Om onze `node_modules` map te wissen, doen we het volgende:

	$ git filter-branch --tree-filter 'rm -rf node_modules' HEAD
	WARNING: git-filter-branch has a glut of gotchas generating mangled history
	 rewrites.  Hit Ctrl-C before proceeding to abort, then use an
	 alternative filtering tool such as 'git filter-repo'
	 (https://github.com/newren/git-filter-repo/) instead.  See the
	 filter-branch manual page for more details; to squelch this warning,
	 set FILTER_BRANCH_SQUELCH_WARNING=1.
	Proceeding with filter-branch...


De map wordt gewist op je filesysteem én in de historiek. Let op, wanneer je via npm opnieuw de `node_modules` koppelt, kun je ze per ongeluk opnieuw adden aan de historiek, wat niet de bedoeling is. We zullen dit vermijden met behulp van een `.gitignore` bestand.

### .gitignore
We zullen nu specifieren welke files we in de toekomst niet meer willen tracken. Dit kan mbv een `.gitignore` file. Dit is een tekstbestand in je repository dat specifieert welke bestanden en mappen genegeerd mogen worden door git.

Maak een nieuw bestand aan met de naam `.gitignore` in de root van je repository. Geef dit de volgende inhoud:

	.DS_Store
	node_modules/

Dit zorgt ervoor dat het bestand `.DS_Store` en de map `node_modules` (& alle submappen van `node_modules` en submappen met deze naam) genegeerd worden in de toekomst.

Add en commit dit bestand, zodat dit mee opgenomen wordt in je repository.

	$ git add -A .
	$ git commit -m "added .gitignore"

In de praktijk zal je als één van je eerste bestanden zo'n `.gitignore` bestand aanmaken. Zo vermijd je dat je repository "vervuild" wordt met onnodige bestanden, en vermijd je ingrijpende acties zoals het verwijderen van mappen & bestanden uit de historiek.
Voor een lijst van nuttige .gitignore files kan je hier terecht: https://github.com/github/gitignore

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

Voer een `git status` uit. Je ziet in het status rapport dat de repository 2 commits achterstand heeft op de online versie:

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

In map 2 (dev3-demo) maken we een nieuw bestand `project2.txt` aan, doen we een add & commit en projecten we te pushen naar de remote:

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
