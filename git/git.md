# Meine Git Notitzen

Die Git Notitzen beziehen sich auf das Handbuch für Git Kurz & Gut 
von O'Reilly und beziehen sich auf die einzelnen Seiten.
Wichtige Kurzbefehle werde ich hier aus quasi als HOW 2 Abtippen.

# Grundlegende Konzepte 
Versionskontrolle muss sein, da es 2 Arten von Menschen gibt.
A) Menschen die noch nicht vom Datenverlust betroffen wurden
B) Die anderen.
Und außerdem will wirklich niemand eine Datei lesen, die final_wirklich_die_letzte_datei ... benannt wurde.
Das ist unsinnig und bring niemandem was.

Git ist dezentral. Das hat den Vorteil, dass wir keinen single Point of failure haben, sondern die Repos mehrmals verteilt werden können.
Das erlaubt merges und Forks, also unterscheidliche private Anpassungen einer Software, ohne dabei ständig eine Netzwerkverbindung haben zu müssen.
Git erstellt Snapshots des jeweiligen Dateisystems. Bei jedem Commit wird eine Vollständige Version des Repos gespeichert.
Git speichert Blobs. Das sind referenzen auf unveränderte vollständige Dateien. Das macht git sehr Effizient im Speicherverbrauch.

## Das Repository
Alle Einstellungen zu dem Repositorium werden im Unterordner .git erstellt.
Es ist möglich Git zentrailisiert zu benutzen und seinen Quellcode über z.B Github auszutauschen.
Oder Gitlab oder Gittea... Per `push` werden Änderungen auf den sich beziehenden Server übertragen und per `pull` werden
Änderungen heruntergeladen.

## Einen Commit Machen
Ein Commit wird wie ein Paket gemacht. Ich habe ein paar Änderugen, die das Projekt betreffen.
Also z.B habe ich mich mit meinen Änderungen um die Anpassung ein paar Konfigurationseinstellungen gekümmert.
Also füge ich einzeln jede Datei, welche ich verändert habe hinzu.
Ich nutze `git add [NAME UND PFAD DER DATEI]` um meine veränderten Einstellungen zusammenzufassen.
Dann dokumentiere ich diese Änderungen und schreibe eine Commit Nachricht. Das kann z.B so aussehen

>chore(config): fixes# 1233 - cleaned unused config entrys
>
>The config entrys were unclean and were seperated into multiple files,
>so that these 2000 Lines could be more easy broken into different pieces.
>Now we got database, filesystem, access and network

Commits sind eindeutig und haben einen Hashwert, das heißt auch der Inhalt des Commits trägt zur Prüfsumme bei.
Git verwendet für die Commit Hashes SHA 256.

## Branch Based Development
Git verwendet Statt Trunks und Revisionsnummern Branches. Es gibt immer eine Hauptkopie, die nennen wir mal master oder main.
Diese Hauptkopie bildet den Aktuellen Versionsstand dar und gilt als "Das Aktuelle System". Das ist das Produktivsystem,
das ist HEILIG. Davon kann man sich Versionen Abzweigen und zur Hautpversion beitragen. Also Quasi einen Branch (zweig) eröffnen,
der dann wieder zum Mutterschiff zurückführt. Da gibt es allerdings eine große Implikation. Je mehr Zeit ich vom Mutterschiff weg
verbringe, desto mehr Äerger wird das verursachen, besonders bei großen Teams und wenn andere auf deine Code Änderungen Warten.
Das ganze hab ich schon n paar mal gehabt.

Es gibt da unterschiedliche Workflows. Einige benutzen Trunk based develeopment, also alle arbeiten auf dem Master mit nur einer Version.
Andere bevorzugen einen GitFlow Workflow, der die Branches ganz granular unterteilt. Nachdem ich jetzt n paar Monate mit SVN gearbeitet
habe muss ich gestehen, dass beide Workflows ihre Berechtigung haben und ich für private Sachen auch eher den Trunk basierten Workflow
gut finde. Also ich Ziehe mir den Aktuellen Main, mache eine Änderung, aktualisiere und so weiter. 

Das macht man in erster Linie, damit man keine Konflikte hat, wer gerade was aktualisiert hat.
Und da sind 2 Sachen wirklich KEY 
1) Committe keinen Scheiß. Lies dir die Sachen durch, die du gemacht hast und trage keinen Murks ein
2) So oft es geht Integrieren. Du hast grad die Aufgabe erledigt? Gut, zeit für ein Update! 
Das hat den Vorteil, dass je öfter du die Arbeit von anderen in deinen Code Integrierst und je näher du am Muttschiff dran bist, 
desto weniger Merge Konflikte musst du lösen.

## Git Konfigurieren
Git Installiert man sich am besten über die Kommandozeile und ist bei den meisten Linux distros 
for free erhältlich (Free as in free beer). Die Konfigurationen werden in 3 Ebenen Hierachisch getroffen
- Lokal (also nur für dieses Repo)
- Global (Nur für diesen Git Benutzer)
- System ( Gilt für alle)

Jeder Git benutzer hat einen Namen und eine Email Adresse also:
`git config --global user.name "Till Kaiser" && git config --global user.email "test@test.de" `
Zum Editieren der Commitnachrichten benutzt git den Standarteditor der jeweiligen Shell.
Wenn ich also nvim ausgewählt habe als Standart Editor, kann ich auch den verwenden.
ich kann den editor aber auch bestimmen. Das geht mit
`git config --global core.editor "code --wait"` ich kann das auch nur mit "nano" machen,
aber so wartet er z.B wenn ich vscode benutzen möchte darauf, dass der editor sich auch öffnet.

## Fork Basierter Workflow
Das ist Interessant für z.B Open Source Projekte. Ich kann auf anderen Plattformen wie Github ein ganzes Repo Klonen
Sagen wir mal ich klone mir die Desktopumgebung LXQT und mache dann auf meinem eigenem Repo die Änderungen. Da die Maintainer von LXQT
mir garantiert keine Rechte geben werden, dass ich das HAupt Repo verändere kann ich mir nach der Copy freedom (danke stallman)
einfach eine Kopie des Projektes ziehen. Meine Kopie kann ich dann immernoch vom Mutterschiff LXQT pullen lassen, dass ich die Änderungen bekomme,
und meine Änderungen kann ich an meinem eigenen Repo machen, sodass wenn ich bereit bin meine Änderungen zu aktualsieren,
kann ich dem HAUPTREPO vorschlagen "Hey ich will, dass du dir mal diesen Code anguckst, den könntest du hinzufügen".

## SSH Basierte Authentifizierung
Prinzipiell sollte bei git mit SSH gearbeitet werden. So ist es möglich, dass nur bestimme Maschienen und bestimme benutzer zugriff auf codeänderungen haben. So kann ein Angreifer selbst wenn er das Passwort eines accouts nennt nicht den Private key des bestimmten rechners
Emulieren, es sei denn er hat zugriff auf den Rechner. (Was ne katastophe ist und dann ist das system sowieso kompromittiert).

Wie das ganze auf Linux eingerichtet wird, kann man sich an jeder Straßenecke nachlesen.
Ich beschreibs hier nur ganz kurz. Es gibt eine cmd util, das ist die ssh-keygen, womit ich einen oder mehrere ssh schlüssel
generieren kann (achtung - höufig wird nur einer verwendet im privatgebrauch) 
Es werden 2 Schlüssel generiert. Privat und public. Ich muss jetzt nicht erwähnen, dass ich meine private parts nicht in der 
Öffentlichkeit teile. Der Public anteil wird also bei github eingepflegt, damit github überprüfen kann: hey das ist mein Rechner.

## Die Gitignore
Git hat ein Ignore Pattern, also dinge, die nicht vom Versionierungssystem betroffen werden sollen.
Das ist vor allem nüzlich, wenn man sowas wie sensible Konfigurationsdaten hat oder gespeicherte dateien, cache usw.
Gitignore kann folgende Dinge ignorieren:
- Eine Datei .env
- node_modules/ (einen ganzen Ordner)
- *.log Alle Dateien mit pattern 
- foo/* alles IN einem Ordner 
Eine Datei die bereits eingechecked ist, aber von nun am ausgeschlossen werden soll, wird entfernt mit
`git rm --cached [NAME UND PFAD DER DATEI]`


## Allgemeine Tipps und Tricks
><b>Tipp:</b> Wenn man sowieso mit dem System git hantiert 
>und das sowieso in der Kommandozeile, lohnt es sich ab und zu mal git status einzugeben,
>so kann man erfahren was gerade der stand des versionssystems ist.

><b>Tipp:</b> Mit `git diff [NAME DER DATEI]` ist es möglich von einzelnen dateien die Änderungen im vergleich zum letzten Stand 
>zu beobachten. Das ist wirklich nützlich wenn man seine Änderungen nochmal durchsehen will.

Das Patchen mit Git kann auch automatisiert geschehen. Ich kann mittels `git add -p` stückweise alles hinzufügen, was
ich für den code geschrieben habe. Das heißt ich kann bei jedem chunk code dann entscheiden, ob ich den haben will oder nicht.
Was echt praktisch ist, wenn ich viele kleine Änderungen gemacht habe.

Ich kann Dateien auch vom Staging wieder entfernen, sodass sie nicht comitted werden, wenn ich das nicht möchte.
So kann ich zumindest eine weitere Hürde vor den Production Code stellen (dass kein Murks committed wird).
Das geht mit `git reset [NAME DER DATEI]`

## Branches
In Git kann ich mit `git checkout -b [NAME/DES/BRANCHES]` einen branch erstellen.
Mit `git branch -m [NEUER/NAME]` kann ich einen branch umbenennen. Und mit `git checkout [NAME/DES/BRANCH]`kann ich den aktuellen
branch umbenennen. 

## Merge
Ein Merge ist die Operation die Arbeit, die ich in einer Abzweigung gemacht habe zu einem Anderen branch hinzuzufügen.
Daher kommt auch der Mergekonflikt. Also wenn ich 2 unterschiedliche Versionsstände habe, muss ich klären, wann welcher code verwendet wird.
Das gilt es absolut und unter allen Bedingungen zu vermeiden. Denn Mergekonflike und grade drastische Mergekonflike geschehen nur, wenn jemand 
sich zu lange Zeit für einen Branch nimmt oder man nicht regelmäßig aktualisiert. 
Ein Merge also zusammenschluss wird durchgeführt, indem ich auf den Branch welchsel, welcher die Änderungen erhalten soll.
Dann wirke ich `git merge [NAME/DES/BRANCH]` und füge daruch die Änderungen hinzu.

## Mergekonflikte
Falls solche Mergekonflikte auftreten: und es kann und wird passieren ist es besonders wichtig nicht überschnell etwas zu entscheiden.
Das beste was man da machen kann, ist es sich einen wirklich <b>VERNÜNFTIGEN</b> Merge editor zuzulegen, der 
dir anzeigt, wie das Fertige File aussehen würde, wenn man die Aktuellen Änderungen durchführen würde. 
Prinzipiell: Kann man fremde Änderungen durchwinken, eigene Änderungen durchwinken oder beides nehmen. 
Jedes mal wird überprüft, ob denn der Code egal aus welcher Richtiung er kommt.

## Rebase
Wenn die Arbeit dann doch nochmal länger dauert und ich noch nicht fertig bin,
aber trozdem aktualisieren muss, kann ich rebasen. Also dem Branch eine neue Abstammung geben.
Das kann zu mergekonflikten führen, da die Anderen, welche in der Zeit änderungen getätigt haben,
ja garnicht wissen, was ich an Änderungen habe. Damit ich ungestört weitermachen kann, integriere ich mit dem rebase
einfach die Änderungen und packe meine Änderungen oben drauf. Das kann wenn die gleichen Dinge bearbeitet werden natürlich zu Mergekonflikten
führen. Aber so kann ich auch mal Länger auf einem Ausgecheckten branch arbeiten (was es trotzdem zu vermeiden gilt).

## Cherry Pick 
mit `git cherry-pick --no-commit [HASH]`kann ich einzelne Änderungen von anderen Branches in mein Arbeitsverzeichnis 
Integrieren. Wenn mir z.B einfällt Jaaaa damals da hatte ich da doch ne Klasse dafür. Die hab ich aber gelöscht weil X
und wurde nicht mehr gebraucht weil Y die hole ich jetzt wieder ins Leben. Das ist da so der usecase für cherrypick.

## Git stash
Ich kann die aktuellen Änderungen mit `git stash` cachen. So kann ich sachen zwischendrin machen oder sonstiges.
Kann hald einen Puffer aufbauen. und mit git stash apply kann ich die Änderungen wieder hinzufügen.
Das habe ich häufig gemacht, wenn ich Änderungen von Außen integrieren möchte mit nem Rebase. Also
erst ALLE Änderungen stashen, dann den rebase durchführen und dann haue ich meine Änderungen da wieder drauf und integriere meine
Änderungen einfach in den Aktuellen Code. Das geht dann mit `git stash apply`

## Wartung und Historie
`git log` und `git reflog` sind 2 wertvolle waffen, um die Commithistorie nachvollziehen zu können.
Ich persönlich finde es wichtig, dass die komplette Commit historie immer vollständig erhalten bleibt.
So können später auch fuck ups wieder rekonstruiert werden und so kann auch nix verloren gehen :)

Mit `git blame [NAME DER DATEI]` kann ich herausfinden, wer zuletzt an der aktuellen Datei
dran war (suprise ich bins die meiste zeit selber).
