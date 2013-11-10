# Git #
## Over Git ##
Git is een versiebeheersysteem. Het laat je onder andere toe om met meerdere mensen samen te werken aan projecten en een historiek van het project bij te houden.

Het werd gelanceerd in april 2005 door Linus Torvalds - de vader van Linux. Codebeheersystemen waren niets nieuws, enkele belangrijke systemen in het verleden waren:

* SCSS begin de jaren 70
* RCS begin de jaren 80
* CVS werd gelanceerd in 1986
* SVN in 2001

De Linux ontwikkeling gebeurde in de beginjaren met Bitkeeper VCS. In 2005 legde Bitkeeper echter enkele extra restricties op aan de gratis open source versie, waardoor Linux niet langer via dit systeem ontwikkeld kon worden. Linus zocht naar alternatieven, maar vond er geen die voldeden aan z'n eisen:

* Eenvoudig aan distributed development doen
* Scalable zijn: met meer dan 1000 ontwikkelaars samen kunnen werken
* Snel & Efficient en betrouwbaar zijn
* Weten wie wat gedaan heeft
* Ondersteuning voor transacties: meerdere acties bundelen
* Branching ondersteuning: afsplitsingen van het project die terug samengevoegd kunnen worden met het hoofdproject.
* Distributed repositories: project met historiek wordt niet centraal bijgehouden.
* Gratis

Toen hij geen alternatief vond die aan deze requirements voldeed besloot hij z'n eigen systeem te ontwikkelen: GIT was geboren.

De naam GIT is geen afkorting, maar een verwijzing naar Linus zelf: het is slang voor "een onaangenaam persoon". Net zoals Linux, wou hij een naam die naar zichzelf verwijst. Nadien is er door de community de afkorting "Global Information Tracker" op geplakt.

## Interne werking ##

Je bestanden worden opgeslaan in een repository. Deze repository bevat informatie over de inhoud van de bestanden, hun naam, locatie en de historiek. 

Van alle files in de repository wordt zowel de naam van de file als de inhoud gehashed via SHA1. Deze 2 hashcodes worden gebruikt om de naam & inhoud van de files op een snelle manier op te halen. Dit zorgt er ook voor, dat identieke files of dezelfde filenames niet dubbel worden opgeslaan, maar gewoon via dezelfde hashcode verwijzen naar dezelfde informatie.

De kans dat twee verschillende bestandsnamen of twee verschillende inhouden van bestanden dezelfde hash code genereren is verwaarloosbaar: dit bedraagt slechts 1/2<sup>160</sup>.

## Een eerste repository

We zullen git gebruiken vanaf de command line. Er zijn wel enkele applicaties die toelaten om via een GUI git commando's uit te voeren, maar wanneer je meer geavanceerde acties wil uitvoeren zul je sowieso terug moeten grijpen naar de command line.

Zorg er eerst en vooral voor dat je git kan gebruiken via de command line. Je kan ondersteuning voor git downloaden en installeren van op [http://git-scm.com/downloads](http://git-scm.com/downloads).

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

Dit zijn enkele basiscommando's die je als je broekzak moet kennen. Dit is niets git-specifiek! Je zal deze commando's ook gebruiken wanneer je later aan de slag gaat met nodejs en grunt.

### Aanmaken van een nieuwe git-repository

Je kan van elke bestaande map een git repository maken met het `git init` commando. Het maakt niet uit of hier al bestanden of submappen in aanwezig zijn. Wij zullen starten met een nieuwe lege map, maar weet dat dit niet nodig is om een project via git te beheren.

Maak een nieuwe map aan en maak hiervan een git repository (opmerking: de dollartekens duiden erop dat dit over een command line input gaat door de gebruiken, en typ je niet):

	$ mkdir project
	$ cd project
	$ git init
	Initialized empty Git repository in /Users/wouter/Documents/project/.git/

Het `git init` commando zal een verborgen map  met de naam .git aanmaken. Hierin zit alle informatie over de repository & z'n historiek.

Via het `git status` commando kun je wat meer informatie opvragen over de huidige status van de repository. Dit gebruik je vaak om te zien welke bestanden er gewijzigd zijn, of er nieuwe bestanden zijn, of er bestanden gewist zijn.

	$ git status
	# On branch master
	#
	# Initial commit
	#
	nothing to commit (create/copy files and use "git add" to track)

### Bestanden tracken & committen

Maak een nieuw bestand hello.txt aan met de tekst "hello world":

	$ echo "hello world" > hello.txt
	
Voer opnieuw het `git status` commando uit:

	$ git status
	# On branch master
	#
	# Initial commit
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
	# Initial commit
	#
	# Changes to be committed:
	#   (use "git rm --cached <file>..." to unstage)
	#
	#	new file:   hello.txt
	#

Nu is git op de hoogte van die file. Dit wil nog niet zeggen dat git automatisch van elke wijziging aan die file een snapshot zal nemen. Je moet zelf beslissen wanneer je een snapshot zal nemen van de wijzigingen in je bestand(en) en deze wil toevoegen aan je git historiek. Dit doe je door een commit uit te voeren:

	$ git commit -m "eerste commit"
	[master (root-commit) 860a909] eerste commit
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
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Git heeft gedetecteerd dat er wijzigingen zijn gebeurd aan een reeds getracked bestand. Je zal deze opnieuw moeten "adden", om deze wijzigingen in de wachtrij te zetten voor een commit (wordt stage for commit genoemd):

	$ git add hello.txt

Commit vervolgens deze wijzigingen:

	$ git commit -m "world gewijzigd naar devine"
	[master bd4b500] world gewijzigd naar devine
	 1 file changed, 1 insertion(+), 1 deletion(-)

Je kan natuurlijk ook meerdere wijzigingen in 1x adden en committen. Pas de tekst aan, en maak een tweede file aan:

	$ echo "hello cp3" > hello.txt
	$ echo "hello" > world.txt
	
Git status zal nu 2 zaken rapporteren: het wijzigen van een reeds getrackte file, en het detecteren van een nieuwe file die nog niet getracked wordt:

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
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
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	modified:   hello.txt
	#	new file:   world.txt
	#

Nu zijn beide gestaged voor commit, en kan je met 1 commit ze loggen in de git repository:

	$ git commit -m "welcome cp3 + new world file"
	 2 files changed, 2 insertions(+), 1 deletion(-)
	 create mode 100644 world.txt

### git add -u . ###

We hebben al eerdere gezien dat je met `git add .` alle wijzigingen kunt stagen voor commit. Nu is het zo dat deletes (wissen van files) niet mee gestaged worden. Doorvoor moet je nog de flag -u toevoegen aan het commando.

Je zal meestal `git add -u .` uitvoeren nadat je `git add .` uitvoerde, om ervoor te zorgen dat ook deletes gestaged worden voor commit.

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
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#	modified:   hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Je krijgt hier al een hint hoe je de wijzigingen in je working directory kunt ongedaan maken: via het git checkout commando. Voer dit commando uit, en controleer de status van de repository:

	$ git checkout hello.txt
	$ git status
	# On branch master
	nothing to commit (working directory clean)

De wijzigingen aan hello.txt zijn ongedaan gemaakt. Als je de inhoud van de file bekijkt via het cat commando, zul je zien dat deze de inhoud bevat van je laatste commit:

	$ cat hello.txt
	hello cp3

### Wijzigingen na staging ongedaan maken

Pas de tekst opnieuw aan naar "hello devine", stage deze wijzigingen via het add commando, maar commit deze nog niet:

	$ echo "hello devine" > hello.txt
	$ git add hello.txt
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	modified:   hello.txt
	#

Je krijgt een hint hoe je deze wijzigingen kunt unstagen: via git reset HEAD:

	$ git reset HEAD hello.txt
	Unstaged changes after reset:
	M	hello.txt

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

	$ git checkout hello.txt

### Commits ongedaan maken

Stel: je hebt bepaalde wijzigingen gecommit, maar om een of andere reden wil je die ongedaan maken.

	$ echo "hello devine" > hello.txt
	$ git add hello.txt
	$ git commit -m "changed, but not sure about it"

Je kan 2 dingen doen: ofwel een nieuwe commit maken die de wijzigingen uit de vorige commit ongedaan maakt (`git revert HEAD`), ofwel de commit volledig uit de historiek gaan wissen (`git reset --hard referentie-naar-commit`).

	$ git revert HEAD

Je terminal zal nu een vim editor tonen, waarin je een commit message kan typen. Pas eventueel de default message aan, en typ `:quit` wanneer je klaar bent.

	[master ad78401] Revert "changed, but not sure about it"
	 1 file changed, 1 insertion(+), 1 deletion(-)

De file zal nu de inhoud bevatten van voor de laatste commit.

Je kan trouwens de commit historiek van een repository bekijken via het `git log` commando:

	$ git log
	commit ad78401ab771bea7425e08b9dc1a68fd96fb5bbf
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Wed Nov 6 09:53:16 2013 +0100
	
	    Revert "changed, but not sure about it"
    
	    This reverts commit f7e3f95692171c5c6dd6a9314f3acfc7354c3559.
	
	commit f7e3f95692171c5c6dd6a9314f3acfc7354c3559
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Wed Nov 6 09:42:31 2013 +0100
	
	    changed, but not sure about it
	
	commit a528ba56e7da390e37e28b1c9af938ba84f82c10
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Tue Nov 5 17:41:41 2013 +0100
	
	    welcome cp3 + new world file
	
	commit bd4b50051584138951ff43c332fffb5d1161d287
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Tue Nov 5 12:06:28 2013 +0100
	
	    world gewijzigd naar devine
	
	commit 860a90914f97666fd0020713b564467ca89b749d
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Tue Nov 5 11:45:20 2013 +0100
	
	    eerste commit

Je ziet dat de "foute" commit nog steeds in de git historiek aanwezig is, en dat de wijzigingen via een nieuwe commit ongedaan gemaakt werden. Merk ook op dat elke commit een unieke SHA1-hash id heeft. Deze ids kun je gebruiken om commits te specifiëren bij bepaalde commano's.

Een meer drastische manier om commits ongedaan te maken, is via het `git reset` commando. Via git reset ga je je working tree gaan resetten naar een bepaalde commit en alle commits na die commit wissen uit de repository.

We willen terug naar de status gaan van onze commit "welcome cp3 + new world file". Via git log, komen we te weten dat het SHA1 id `a528ba56e7da390e37e28b1c9af938ba84f82c10` is. Specifieer het SHA1 id van de commit naar waar je wil resetten na het commando. Je hoeft niet het ganse id te specifiëren: de eerste 4 karakters zijn vaak voldoende (ten minste als deze uniek zijn):

	$ git reset --hard a528
	HEAD is now at a528ba5 welcome cp3 + new world file

Wanneer je nu opnieuw git log uitvoert, zie je dat de commits na a528 verdwenen zijn:

	$ git log
	commit a528ba56e7da390e37e28b1c9af938ba84f82c10
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Tue Nov 5 17:41:41 2013 +0100
	
	    welcome cp3 + new world file
	
	commit bd4b50051584138951ff43c332fffb5d1161d287
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Tue Nov 5 12:06:28 2013 +0100
	
	    world gewijzigd naar devine
	
	commit 860a90914f97666fd0020713b564467ca89b749d
	Author: Wouter Verweirder <wouter@aboutme.be>
	Date:   Tue Nov 5 11:45:20 2013 +0100
	
	    eerste commit

Zo'n `git reset` commando ga je enkel gebruiken om lokale commits ongedaan te maken. Eens je samenwerkt met anderen, en commits reeds verspreid zijn onder andere users, dan gebruik je het `git revert` commando om een nieuwe commit te maken die een vorige commit ongedaan maakt.

## Samenwerken met git

Tot nu toe hebben we lokaal gewerkt met git. Je kan ook met meerdere mensen samenwerken aan 1 repository door te werken met een remote server. Iedereen heeft een lokale kopie van de repository staan, en kan zijn wijzigingen via een remote server gaan synchronizeren met andere mensen die de repository hebben staan.

In principe kan je elke computer waarop je de git command tools hebt geïnstalleerd gebruiken als server. Het is dan alleen niet zo praktisch om samen te werken van thuisuit, je moet er dan voor zorgen dat je computer extern bereikbaar is en iedereen die samenwerkt moet dan je ip adres of hostname weten.

Daarom maken we gebruik van een hosted git omgeving. Hier zijn meerdere opties voor, wij zullen gebruik maken van GitHub.

### Aanmaken & linken GitHub account

We zullen eenmalig een GitHub account aanmaken en onze GitHub credentials linken aan onze computer, zodat we niet telkens opnieuw ons wachtwoord moeten ingeven.

Surf naar [https://github.com](https://github.com) en maak een account aan. Vraag daarna op [https://github.com/edu](https://github.com/edu) een education plan aan, dit zal handig zijn om private repositories aan te maken.

Open daarna een terminal window. We zullen onze naam & email adres koppelen aan git, zodat git weet wie een commit uitvoert. Zorg dat je email adres het adres is dat je gebruikte om je GitHub account aan te maken:

	$ git config --global user.name "Your Name Here"
	$ git config --global user.email "your_email@example.com"

Daarna configureren we git om gebruik te maken van onze OSX keychain om paswoorden op te slaan:

	$ git config --global credential.helper osxkeychain

### Repository aanmaken & eerste push

Login op je GitHub account, en klik op de "New repository" button. Kies een naam voor je repository en klik op de "Create Repository" button.

Open een terminal venster en navigeer via cd commandos naar de map van de git repository met de hello world files. We zullen er voor zorgen dat we onze lokale repository via GitHub kunnen synchronizeren, door een "remote" te adden. Een remote is een lokatie waarmee je een git repository kan synchronizeren:

	$ git remote add origin https://github.com/devinehowest/git-demo
	$ git push -u origin master
	Counting objects: 10, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (4/4), done.
	Writing objects: 100% (10/10), 742 bytes, done.
	Total 10 (delta 0), reused 0 (delta 0)
	To https://github.com/devinehowest/git-demo
	 * [new branch]      master -> master
	Branch master set up to track remote branch master from origin.

Het `git push` commando zal lokale, niet-gesynchronizeerde wijzigingen uploaden naar de remote lokatie. Het -u attribuut gebruik je de allereerste keer, om ervoor te zorgen dat je bij toekomstige synchonizaties de remote name niet meer moet opgeven. Je kan dan in de toekomst gewoon `git push` uitvoeren.

### Git add - commit - push

Vanaf nu kun je commits gaan pushen naar de online repository. Meestal bundel je verschillende lokale commits wanneer je gaat pushen. Dit hebben we in feite reeds gedaan met onze eerste push: alle commits die we eerder uitvoerden, staan nu ook op de online repository.

Wis het world.txt bestand, add & commit. We maken gebruik van `git add -u .` om ervoor te zorgen dat de delete actie van die file gestaged wordt:

	$ rm world.txt
	$ git add -u .
	$ git commit -m "removed world file"
	[master 299abcd] removed world file
	 1 file changed, 1 deletion(-)
	 delete mode 100644 world.txt

Maak een README.md bestand aan, met een beetje info over de repository:

	$ echo "Demo repository" > README.md
	$ git add .
	$ git commit -m "added readme file"
	[master 9ed12bf] added readme file
	 1 file changed, 1 insertion(+)
	 create mode 100644 README.md

Voer een git status uit. Je ziet in het status rapport dat de repository 2 commits achterstand heeft op de online versie:

	# On branch master
	# Your branch is ahead of 'origin/master' by 2 commits.
	#
	nothing to commit (working directory clean)

Doe een `git push` om je commits op GitHub te plaatsen:

	Counting objects: 6, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (5/5), 506 bytes, done.
	Total 5 (delta 0), reused 0 (delta 0)
	To https://github.com/devinehowest/git-demo
	   a528ba5..9ed12bf  master -> master

Wanneer je de repository via je browser bekijkt, zal je zien dat de inhoud van de README.md file, getoond wordt onder de lijst van files. Dit is een bestand in het MarkDown formaat. Markdown is een eenvoudige markup taal om documenten op te maken. Meer informatie hierover kan je onder andere vinden op wikipedia: [http://en.wikipedia.org/wiki/Markdown](http://en.wikipedia.org/wiki/Markdown).

### Bestaande repository binnenhalen

Eens een repository aangemaakt is, en op een server zoals GitHub staat, kun je hem ook op andere computers / locaties binnenhalen. De repository een eerste keer binnenhalen doe je via het `git clone` commando. Vanaf dan kun je updates binnenhalen via het `git pull` commando. `git pull` is het omgekeerde van `git push`, en zal je gebruiken om updates die je nog niet lokaal hebt staan binnen te halen.

Open een tweede terminal venster, navigeer naar de bovenliggende map van je originele git repository en maak een map aan waarin je een duplicaat van de repository zal clonen:

	$ mkdir project2

Voer het git clone commando uit, om de online repository binnen te halen:

	$ git clone https://github.com/devinehowest/git-demo project2
	Cloning into 'project2'...
	remote: Counting objects: 15, done.
	remote: Compressing objects: 100% (7/7), done.
	remote: Total 15 (delta 0), reused 15 (delta 0)
	Unpacking objects: 100% (15/15), done.

Je hebt nu 2 clones van dezelfde repository op je computer. Eentje in de map project en eentje in de map project2. We zullen deze twee gebruiken om synchronisaties en merges te testen.

### push - pull

We simuleren samenwerken met 2 users door op in twee verschillende mappen met dezelfde remote te synchronizeren. Let bij de volgende acties op in welke map je de nodige commando's uitvoert. (de project map staat vanaf nu telkens voor het dollarteken in het uit te voeren commando).

In map 1 maken we een nieuw bestand project.txt aan, we adden, committen en pushen naar de remote:

	project$ echo "created in project" > project.txt
	project$ git add .
	project$ git commit -m "added project.txt file"
	[master a93634a] added project.txt
	 1 file changed, 1 insertion(+)
	 create mode 100644 project.txt
	project$ git push
	Counting objects: 4, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 335 bytes, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To https://github.com/devinehowest/git-demo
	   9ed12bf..a93634a  master -> master

In map 2 maken we een nieuw bestand project2.txt aan, doen we een add & commit en projecten we te pushen naar de remote:

	project2$ echo "created in project2" > project2.txt
	project2$ git add .
	project2$ git commit -m "added project2.txt file"
	[master eac21f9] added project2.txt file
	 1 file changed, 1 insertion(+)
	 create mode 100644 project2.txt
	project2$ git push
	To https://github.com/devinehowest/git-demo
	 ! [rejected]        master -> master (non-fast-forward)
	error: failed to push some refs to 'https://github.com/devinehowest/git-demo'
	hint: Updates were rejected because the tip of your current branch is behind
	hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
	hint: before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.

We krijgen een fout: er zijn nieuwe commits op de remote, die we nog niet hebben binnengehaald in onze project2 clone. We moeten deze eerst pullen, voor we een push kunnen doen:

	project2$ git pull

We krijgen een vim editor te zien om een merge uit te voeren. Je kan hier een custom message ingeven. Geef `:quit` in om de vim editor te sluiten en verder te doen met de merge.

	remote: Counting objects: 4, done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 3 (delta 0), reused 3 (delta 0)
	Unpacking objects: 100% (3/3), done.
	From https://github.com/devinehowest/git-demo
	   9ed12bf..a93634a  master     -> origin/master
	Merge made by the 'recursive' strategy.
	 project.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 project.txt

Wanneer je een git status uitvoert, zal je zien dat je 2 commits voor bent op de remote: 1 commit is de merge commit, en een tweede commit is de project2.txt commit:

	project2$ git status
	# On branch master
	# Your branch is ahead of 'origin/master' by 2 commits.
	#
	nothing to commit (working directory clean)

Doe opnieuw een push van die commits naar de remote. Het pushen lukt deze keer wel:

	project2$ git push
	Counting objects: 7, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (4/4), done.
	Writing objects: 100% (5/5), 546 bytes, done.
	Total 5 (delta 2), reused 0 (delta 0)
	To https://github.com/devinehowest/git-demo
	   a93634a..58096ca  master -> master

Haal nu deze commits ook op in je eerste map via een `git pull` commando:

	project$ git pull
	remote: Counting objects: 7, done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 5 (delta 2), reused 5 (delta 2)
	Unpacking objects: 100% (5/5), done.
	From https://github.com/devinehowest/git-demo
	   a93634a..58096ca  master     -> origin/master
	Updating a93634a..58096ca
	Fast-forward
	 project2.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 project2.txt

### rebase

Wij zullen voorlopig werken met een centralized workflow: we werken met meerdere mensen samen op 1 master branch via 1 remote. Er zijn nog andere, meer geavanceerde workflows die werken via branches en forks. Deze zijn echter al iets complexer, wij zullen ons voorlopig houden aan de centralized workflow.

In het voorgaande scenario hebben we een merge commit toegevoegd om een niet up-to-date repository te fast-forwarden. Deze is bij een centralized workflow overbodig: we kunnen beter gebruik maken van een rebase bij de git pull. Een rebase zal eerst alle commits van de remote uitvoeren, en jouw commits erachter uitvoeren, in plaats van standaard een merge commit uit te voeren.

Doe een delete van project.txt in de project map:

	project$ rm project.txt
	project$ git add -u .
	project$ git commit -m "removed project.txt"
	[master 59bfb66] removed project.txt
	 1 file changed, 1 deletion(-)
	 delete mode 100644 project.txt
	project$ git push
	Counting objects: 3, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (2/2), 230 bytes, done.
	Total 2 (delta 1), reused 0 (delta 0)
	To https://github.com/devinehowest/git-demo
	   58096ca..59bfb66  master -> master

Doe daarna een delete van project2.txt in de project2 map. We zullen ook hier eerst een pull moeten doen voordat we kunnen pushen. Het verschil bij de pull is dat we een rebase flag meegeven, om ervoor te zorgen dat eerst alle commits van de remote repository uitgevoerd worden, en daarna onze eigen commits:

	project2$ rm project2.txt
	project2$ git add -u .
	project2$ git commit -m "removed project2.txt"
	[master 9cae76e] removed project2.txt
	 1 file changed, 1 deletion(-)
	 delete mode 100644 project2.txt
	project2$ git pull --rebase
	remote: Counting objects: 3, done.
	remote: Compressing objects: 100% (1/1), done.
	remote: Total 2 (delta 1), reused 2 (delta 1)
	Unpacking objects: 100% (2/2), done.
	From https://github.com/devinehowest/git-demo
	   58096ca..59bfb66  master     -> origin/master
	First, rewinding head to replay your work on top of it...
	Applying: removed project2.txt

Op deze manier wordt er geen merge commit aangemaakt. Wanneer je een git status uitvoert, zie je dat je nu maar 1 commit voorsprong hebt op de remote repository, in plaats van 2:

	project2$ git status
	# On branch master
	# Your branch is ahead of 'origin/master' by 1 commit.
	#
	nothing to commit (working directory clean)

Push naar de remote repository. Doe ook opnieuw een pull in de project map, zodat beide repositories up-to-date zijn.

## Merge conflicts

Tot nu toe hebben we braafjes in aparte files wijzigingen aangebracht. Het kan echter gebruiken dat je met 2 personen in dezelfde file wijzigingen hebt aangebracht, en dat er een conflict optreedt.

Pas in de project map de tekst aan in hello.txt en push deze naar de remote repository:

	project$ echo "edit in project" > hello.txt
	project$ git add .
	project$ git commit -m "changed hello.txt"
	[master 7f3b200] changed hello.txt
	 1 file changed, 1 insertion(+), 1 deletion(-)
	project$ git push
	Counting objects: 5, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 303 bytes, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To https://github.com/devinehowest/git-demo
	   487257a..7f3b200  master -> master	

Pas nu ook in de project2 map de tekst in dezelfde file aan en probeer te pushen:

	project2$ echo "edit in project2" > hello.txt
	project2$ git add .
	project2$ git commit -m "changed hello.txt in project2"
	[master 599d7b0] changed hello.txt in project2
	 1 file changed, 1 insertion(+), 1 deletion(-)
	project2$ git push
	To https://github.com/devinehowest/git-demo
	 ! [rejected]        master -> master (non-fast-forward)
	error: failed to push some refs to 'https://github.com/devinehowest/git-demo'
	hint: Updates were rejected because the tip of your current branch is behind
	hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
	hint: before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.

We moeten eerst nog pullen, voor we kunnen pushen:

	project2$ git pull --rebase
	remote: Counting objects: 5, done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 3 (delta 0), reused 3 (delta 0)
	Unpacking objects: 100% (3/3), done.
	From https://github.com/devinehowest/git-demo
	   487257a..7f3b200  master     -> origin/master
	First, rewinding head to replay your work on top of it...
	Applying: changed hello.txt in project2
	Using index info to reconstruct a base tree...
	M	hello.txt
	Falling back to patching base and 3-way merge...
	Auto-merging hello.txt
	CONFLICT (content): Merge conflict in hello.txt
	Failed to merge in the changes.
	Patch failed at 0001 changed hello.txt in project2
	The copy of the patch that failed is found in:
	   /Users/wouter/Documents/project2/.git/rebase-apply/patch
	
	When you have resolved this problem, run "git rebase --continue".
	If you prefer to skip this patch, run "git rebase --skip" instead.
	To check out the original branch and stop rebasing, run "git rebase --abort".

We krijgen een merge conflict, doordat we in beide repositories dezelfde file wijzigden. We moeten eerst dit conflict oplossen, voordate de rebase kan verderdoen.

Via `git status` kun je een lijst opvragen met de merge conflicts:

	project2$ git status
	# Not currently on any branch.
	# You are currently rebasing.
	#   (fix conflicts and then run "git rebase --continue")
	#   (use "git rebase --skip" to skip this patch)
	#   (use "git rebase --abort" to check out the original branch)
	#
	# Unmerged paths:
	#   (use "git reset HEAD <file>..." to unstage)
	#   (use "git add <file>..." to mark resolution)
	#
	#	both modified:      hello.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

Je krijgt de melding dat je aan het rebasen bent. Bij Unmerged paths zie je de files die in conflict zijn. Je moet eerste het conflict oplossen, door de file te editen, voor je kan verder doen met de rebase.

Open het txt bestand in een teksteditor. Je zal zien dat zowel de content uit project als project2 aanwezig is:

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

Wanneer je nu een git status uitvoert, zal je zien dat je opnieuw op de master branch zit, en 1 commit voorsprong hebt op de remote:

	project2$ git status
	# On branch master
	# Your branch is ahead of 'origin/master' by 1 commit.
	#
	nothing to commit (working directory clean)

Nu kan je opnieuw pushen naar de remote:

	project2$ git push
	Counting objects: 5, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 326 bytes, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To https://github.com/devinehowest/git-demo
	   7f3b200..920c81f  master -> master

Doe een `git pull` in de andere map, zodat beide mappen terug in sync zijn.

## Git Resources

Dit is een basis introductie om je op weg te helpen met git. Er is nog heel wat meer mogelijk met git & github. Meer informatie & tutorials kun je onder andere vinden op volgende locaties:

* [http://rypress.com/tutorials/git/index.html](http://rypress.com/tutorials/git/index.html)
* [https://www.atlassian.com/git/](https://www.atlassian.com/git/)
* [https://help.github.com/](https://help.github.com/)
* [http://git-scm.com/book](http://git-scm.com/book)