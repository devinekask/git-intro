- [Git](#git)
  * [Over Git](#over-git)
  * [Interne werking](#interne-werking)
  * [Een eerste repository](#een-eerste-repository)
    + [Werken in Terminal](#werken-in-terminal)
    + [Aanmaken van een nieuwe git-repository](#aanmaken-van-een-nieuwe-git-repository)
    + [Bestanden tracken & committen](#bestanden-tracken---committen)
    + [Bestanden wijzigen](#bestanden-wijzigen)
    + [git add -A .](#git-add--a-)
  * [Wijzigingen ongedaan maken](#wijzigingen-ongedaan-maken)
    + [Wijzigingen vóór staging ongedaan maken](#wijzigingen-v--r-staging-ongedaan-maken)
    + [Wijzigingen na staging ongedaan maken](#wijzigingen-na-staging-ongedaan-maken)
    + [Commits ongedaan maken](#commits-ongedaan-maken)
  * [Bestanden negeren](#bestanden-negeren)
    + [Bestanden wissen](#bestanden-wissen)
    + [Bestanden & mappen verwijderen uit je volledige historiek](#bestanden---mappen-verwijderen-uit-je-volledige-historiek)
    + [.gitignore](#gitignore)
  * [Samenwerken met git](#samenwerken-met-git)
    + [Aanmaken & linken GitHub account](#aanmaken---linken-github-account)
    + [Repository aanmaken & eerste push](#repository-aanmaken---eerste-push)
    + [Gitignore aanmaken](#gitignore-aanmaken)
    + [Git add - commit - push](#git-add---commit---push)
    + [Bestaande repository binnenhalen](#bestaande-repository-binnenhalen)
    + [push - pull](#push---pull)
    + [rebase](#rebase)
  * [Merge conflicts](#merge-conflicts)
  * [Git branches](#git-branches)
  * [Git Resources](#git-resources)



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

* de inhoud van bestanden wordt opgeslaan in blob objecten
* de historiek wordt bijgehouden in commit objecten
* de structuur wordt bijgehouden in tree objecten

Wanneer je meerdere files hebt met dezelfde inhoud, dan zal in de tree meerdere keren verwezen worden naar hetzelfde blob object, waardoor er plaats bespaard wordt.

## Een eerste repository

We zullen git gebruiken vanaf de command line. Er zijn wel enkele applicaties die toelaten om via een GUI git commando's uit te voeren, maar wanneer je meer geavanceerde acties wil uitvoeren zul je sowieso terug moeten grijpen naar de command line.

Git wordt mee geïntalleerd wanneer je de xcode command line tools installeert. Indien je dit dus reeds gedaan hebt (bijvoorbeeld om Node.js te laten werken), dan kun je meteen aan de slag. Een andere optie (zonder de command line tools) is git downloaden en installeren van op [http://git-scm.com/downloads](http://git-scm.com/downloads).

### Werken in Terminal

