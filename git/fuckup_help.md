# Meine Fuck Up Behebung
Du hast grade Murks gemacht? Kein Problem, ich geb dir ein paar Mittel zur Fuck up behebung.
Aber pass auf: Das sind keine Patentrezepte. Die funktionieren gut für mich.

## Steh auf und mach eine kurze Pause
Geh vom Rechner weg und zermarter dir nicht den Kopf. Je mehr Ruhe du für bestimmte
Sachen hast, desto besser wird das Ergebnis. Mach keine Hektische Scheiße und 
sorg dafür, dass du nen klaren Kopf hast.

## Besorg dir eine Gummiente oder lass deinen Kollegen zu einer Gummiente werden
Damit ist das "Rubberduck-Debugging" gemeint. Also ich erzähle mein gesamtes Vorhaben 
schritt für Schritt dem Kollegen und wenn der Kollege nicht pennt (am besten schnappt man sich dafür
kurz nen Senior), kann der Kollege dir auch sagen "Hey ich würd das so und so machen"
Denn: Software ist Teamsport

Noch besser: Wenn der Kollege das Pair programming mäßig mit dir Lösen kann,
wenn es sich hierbei um kritische operationen handelt. 2 Hirne denken einfach besser als eins.

## Kopiere keine Kommandos in die Bash, die du nicht zu 100% verstehst!!!
Ich weiß es ist verlockend eine bei Stack Overflow total hochgelobte Antwort zu kopieren und
einfach einzufügen, aber wenn ich mir nicht zu 100% sicher bin, was das macht, sollte ich grade in Fuck Up Situationen
NICHT irgenwelche Kommandos kopieren.

----

Da wir jetzt mögliche Dummheit, Müdigkeit oder sonstigen Unfug als
Fehlerquelle verbannt haben können wir jetzt den Fehler lösen

----
## Steps to Unfuck Git

### Schritt 1: Schau dir den aktuellen Status an
Zur Not ist es auch eine gute Idee einmal aufzuschreiben, was der aktuelle Stand ist.

### Schritt 2: Identifiziere: Wo ist der Fuck Up? Was genau hast du gemacht, was schief gegangen ist?
Sei ehrlich und versuche so vollständig wie möglich zu rekonstruieren, was du getan hast 
und in welcher reihenfolge. So kannst du auch feststellen, was wo kaputt gegangen ist und 
in welcher "Fuck Up Phase" wir uns befinden.

#### Der Fuckup ist im Änderungsindex
Einfach die Änderungen normal bearbeiten. EZ

#### Der Fuckup ist im staging kurz davor zum Commit zu werden
Hol den Lachs vom Feuer mit `git restore --staged [NAME DER DATEI]` 

#### Der Fuckup ist im letzten commit
Einfach `git commit --amend`, nacharbeiten und nochmal ran. Das ist noch der einfache Fall.

#### Der Fuckup ist in einem vorherigem commit
`git revert [HASH]` aber vorsicht: alles was zusätzlich geändert wurde, wird davon mitgenommen.

#### Der Fuckup ist veröffentlich worden
Nimm deinen Mut, gehe zum Repo owner und bitte 1) um Verzeihung und 2) um einen Vorschlag wie 
man das Problem gemeinsam Lösen kann. Denn jetzt ist der Fuck up nicht mehr nur dein Problem, sondern
kann anderen auch den Tag vermiesen. Meistens ist hier die Antwort einen neuen Commit zu erstellen,
der den aktuellen Stand als Hotfix behebt.
