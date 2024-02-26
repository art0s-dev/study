# Clean Code
Das Dokument bezieht sich _naürlich_ auf das werk von robert martin aka "Onkel Bob".

<b>Struktur</b>

Das buch ist grob in 3 Sektionen unterteilt.
Theorie, Praxis und Evaluation. In diesem Dokument werde ich alle 3 bearbeiten.

## Kapitel 1 Clean Code
Code ist geschriebene Spezifikation, Anforderung für den Kunden. Schlechter Code erschwert die weitere Erstellung von Features
und behinder das Wachstum der Anwendung. Es ist menschlicht - wir alle schreiben code "to get shit done", aber genau sowas verursacht das.
Redesigns sind immer vollkommener Bockmist. Es ist immer besser das bestehende Produkt zu verbessern. 

Seine Kernaussage ist im mPrinzip, dass wir selbst schuld sind an verrotendem Code weil wir selbst
uns nicht die Zeit einräumen oder drum kämpfen, dass wir das machen. Also: Immer Estimates n bisschen höher ansetzen und 
Qualitätsverbesserungen einfach im gewissen Rahmen durchführen.

Im Prinzip will Onkel Bob von uns, dass wir selbst ein Gespür für Code smells bekommen.

### Meinungen bekannter Programmierer
Interessanterweise zerfetzt Onkel bob das Zitat von Stroustrup ein wenig.
S. meint, dass Cleancode für ihn Wartungsarm, Selbst regenerierend (Error handling), und von haus aus
Effizient, ohne unsinnige Performance verbesserungen (Sprachdurchfall) hinzuzufügen.
Ebenfalls erwähnt S., dass Clean code eine Sache gut macht, also fokussiert ist.

"Big Dave" hat da eher eine interessantere Definition. Er geht davon aus, dass der nächste damit auch arbeiten kann.
Ebenfalls möchte er, dass eine klare minimale Api zur Verfügung gestellt wird. Auch verlangt er, dass Akzeptanztests gemacht werden.
Also harte Kriterien nach dem der Kunde das Produkt abnimmt - automatisch getestet.

Jon Jeffries (C# dude) -> "Minimizes the number of entities" 
Also nur so viel, wie nötig ist. 

War Cunninghan (Father of Extreme Programming)
es ist clean code, wenn der code genau das mach wie er benannt ist - was man erwartet.
außerdem geht er davon aus, dass wenn die Domäne klar im Code lesbar ist, dass es dann clean code ist.

------
Anmerkung:Onkel bob versucht keinesfalls richtig zu sein, sondern nur guidelines zu geben.
Er kommt ja selbst eher aus der OOP Ecke und er denkt bei Clean Code mehr an Schulen wie Jiu Jitsu, also bestimmte Strömungen.
Das heißt er weiß, dass er nicht die Bundeslade hat. Und er weiß, dass nicht alle seiner Meinung sein werden.
Er fordert dazu auf, auch andere Schulen zu lernen ( functional fällt mir da ein)
------

Onkel bob meint, wir verbringen mehr Zeit mit dem Lesen von Code als mit dem Schreiben von Code.
(Also sollte der Code ja eigentlich die Intention zeigen. Also das Implizite Explizit erwähnen.)
Idee: es gibt in java so wie in vielen Sprachen auch den Nullcheck also if(x == null) { ... 
Es wäre ja eine gute Idee aufzuschreiben _WANN_ X null ist, damit man beim Lesen schon sehen kann,
was die Bedingung beinhaltet oder welche methoden auf die variable zugreifen, es verändern etc.

## Kapitel 2 Benennung


### Intentionale Benennung
Onkel Bob schlägt vor die Benennung direkt an die Domäne zu koppeln.
So werden die Variablen ausdrucksstärker und geben direkt an, was die Variablen beinhalten.
(... oder methoden)

### Keine Missinformation
HashMap<Accounts> accountList = new HashMap<>(); // Merkste selber wa?
Also es ist keine Liste! Es ist schlichtweg irreführend

Genau so Tödlich ist die Olle Namensverkettung(Is irgendwie so ne OOP Krankheit)
SalesOrderItemSplitMigrationManager
SalesOfferItemSlpitMigrationManager
Auch hier wieder die haben den Gleichen Shape aber es ist eine andere Klasse.
Die Namen unterscheiden sich nicht gut genug. Sie sind nicht "griffig"

### Mach Unterschiede
Keine Noise Words sowas wie A oder The oder An. Der Variablenname muss im Prinzip den Existenzberechtigungsausweis immer bei sich tragen.
Auch im Bezug wenn du 3 sehr Ähnliche Funktionen hast
getAccount()
getAccountList()
getAccountInfo() 
Ja herrgott welche davon soll ich denn jetzt benutzen???

### Benutze Aussprechbare Namen
Hey das Erstellungsdatum vom Kundendatensatz 112 ist auf morgen gestellt - is aussagekräftiger als
Hey genYMDHMS: in der DtaRc102 ist auf morgen gestellt.

### Benutze Suchbare Namen
MAX_CLASSES_PER_STUDENT lässt sich besser suchen als 7.
Auch I und J in Methoden in Iterationen sollten vermieden werden und stadtdessen sollte der Inhalt doch einfach
als variablenname genommen werden.

### Encodings
Don't. Das ist n warcrime für alle beteiligten
UTF-8, englische Benennung und fertig ist die Kiste

### Hungarian Notation
UUser (Also U für datentyp user) -> Warcrime.
Braucht kein Mensch weil in  der Regel die IDE das zusammendengeln kann.

### Member Prefixes
m_user 
MO_user 
-> Warcrime. Lass es. Wenn du generische Präfixe und Suffixe
für eine Methode brauchs, unterscheidet sie sich einfach nicht stark genug von der anderen und kann
daher zusammengelegt werden 

### Interface und Implementation
I vor nem Interface ist ein warcrime. 
Impl als Implementierung von nem Interface auch. 
Der Name des Interfaces sollte ja eigentlich beschreiben, was das Interface ist.

### Klassennamen
Keine Verben. Manager, Info, Data , Processor sind no Go weil sie nicht klar sind.

### Methodennamen
Möglichst nur Verben. Als Präfix sind get / set und is erlaubt
Keine Quatschnamen (weil nur du das liest). Beschreibe was es macht.

### Keine Doppelten Konzepte
Wenn du eine Controller und eine Manager und eine Driver Klasse hast - wo ist der unterschied zwischen denen?

### Benutze das gleiche Wort für die gleiche Operation
Wenn du eine Methode hast die add heißt und eine methode die insert heißt gehe ich davon aus,
dass sie 2 unterschiedliche dinge tun.

### Benutze Technische Namen
Wenn du z.B Design Patterns verwendetst Nenne doch dann einfach die Klasse AccountVisitor oder so.
So erkennt jedenfalls derjenige der es liest, dass es sich hier um das Visitorpattern handelt und 
kann die klasse besser "scannen" beim lesen

### Benutze Namen aus der Domäne
Wenn der Vorgang den du benutzt in der Domäne einen bestimmten Namen hat (Fakturieren z.B)
dann nenn es auch so. Damit können die Leser das besser verstehen, wenn Sie Domänenwissen haben.
(Im besten Fall schreibst du nen Schnittstellenkommentar mit der Verlinkung zu einem Artikel was gemeint ist)

### Gebe Kontext
Du kannst Lokale Variablen verlängern, indem du klar machst zu WAS die variablen gehören.
Also z.B bei dem Beispiel adresse addressFirstName -> Besser als nur ein wildes first name, weil
du so die namen gruppieren kannst. Noch besser ist es an der Stelle ein Record zu haben, dann kann man sich das Adress davor gleich schenken.

## Funktionen

### Sollten klein sein.
Wenn du Funktionen klein hälst, gruppierst und auf high level ebene benennst, kannst du die intention der Funktion
besser ausdrücken und sie wird so leichter zu lesen. Versuch es so klein es geht zu halten.


