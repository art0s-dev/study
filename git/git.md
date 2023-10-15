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
Das

