#Test Driven Development

Diese Notitzen beziehen sich auf das gleichnamige Buch von Kent Beck. Die Praxisübungen aus dem Buch werde ich
in hexenhammer's testsuite anwenden.

## The Money Problem
### Zum Vorwort

Clean Code der Funktioniert ist gut weil:
- die Entwicklung vorhersagbar ist
- man die Chance hat zu lernen
- es im allgemeinen die Softwarequalität erhöht

Aber wie schafft man eigentlich Clean Code, welcher funktioniert? Die Antwort ist die testgetriebene Entwicklung weil
mit automatisieren Tests die Funktionalität des Codes bewiesen werden kann.
In der testgetriebenen Entwicklung wird neuer Code geschrieben, wenn ein automatischer Test versagt hat.
Ebenfalls ist es das Ziel Duplikate zu eleminieren.

Das hat folgende Bedingungen zur Folge:
- der Designprozess ist fließend und inkrementell
- Wir schreiben unsere Tests selber
- Unsere IDE muss auf jede Änderung sofort reagieren
- Die architektur muss lose gekoppelt sein, um das Testen zu vereinfachen

Daraus resultiert folgende Methodik:
- Red (Schreibe einen Test der nicht funktioniert)
- Green (Bringe den Test zum funktionieren - durch production code)
- refactor (Aufräumen)

Das hat folgende positive Effekte:
- QA hat weniger Arbeit
- Keine Überraschungen
- mehr Features!

TDD ist auch eine technik die Moral zu erhöhen durch ein gutes tooling. Auch soziales
- Sei konkret
- Kommuniziere klar
- Sei offen für Feedback

TDD sorgt für ein solides "rock solid" Fundament.

### Notitzen zum Geldproblem

Der Author will wirklich, dass man in den Tests, ein möglichst gutes Interface designed.
Der Vorschlag ist es sich wirklich von Test zu Test zu hangeln und sich auch gerne für den Arbeitsprozess
Notitzen zu machen, denn eins nach dem Anderen wird implementiert.

Im Refactoring Step geht es darum Duplikate zu entfernen, aber eigentlich
sind die Duplikate nur ein Symptom. Nehmen wir als Beispiel spezifischen Cod, der Abhängigkeiten erzeugt,
schlechtes Design und leaky abstractions (5 stellen müssen ein Verhalten implementieren statt nur einer Stelle.)
Der Author bedient sich beim Refactoring stark am "klassischen" Klassenaufbau und klassischer OO.


### Degenerate Objects

Der Author bezieht sich auf die 3 Stufen des Testens: 
- Ein gutes Interface
- Eine schnelle Lösung (schreib dir die gute Lösung auf, mach aber die schnelle)
- Implementier die gute Lösung statt des Provisoriums

Beck schlägt vor, dass es okay ist auch mal bestehende Tests zu überdenken oder zu ändern.
Man kann ja nicht immer nen guten Tag haben und mit "gutem" Design richtig liegen.

Es ist ebenfalls möglich um einen Test grün zu bekommen, Werte mit Konstanten zu belegen, statt der eigentlichen Implementierung,
WENN es hinterher durch die Implementierung ausgetauscht wird. So wird man flexibler.
Der Vorteil liegt darin, dass man so viel eher ein Gespür dafür bekommt, wie sich das System verhalten soll.

### Equality for all
Anbei Value Objekte Sind ein Pattern, allerdings haben sie eine Bedingung. Sie müssen immutable sein.

>Wenn man in Java Objekte vergleichen will muss man equals und hash code
>als methode implementieren

Beck spricht von Triangulation, wobei er bemisst, wie sich das Inferface verhalten soll und wie es 
sich NICHT verhalten soll. Also nimmt er neben AsserTrue auch Assert False in den selben Test rein.
Ebenfalls wird empfohlen encapsulation wirklich zum Vorteil zu nutzen, da so das Interface klarer wird.

### Franc-ly speaking
Copypasta ist erlaubt, WENN ich es hinterher aufräume. Make it run, then make it right.

## Equality for all, Redux
Es wird vorgeschlagen Gemeinsamkeiten durch Vererbung in einer Superklasse zusammenzuführen.
So kann man sich die Duplikation sparen. Sei ehrlich mit deinen Tests. Auch wenn du Angst davor hast,
unliebsame Fälle zu testen, musst du es trotzdem tun, da du sonst nicht versichern kannst, dass dein Code nach
einem Refactoring noch funktioniert. "Write the tests you wish you had"
Wer legacy Codebases kennt, kennt das nur zu gut.

### Apples and Oranges
Der Author versucht im Beispiel die Methode equals für die unterschiedlichen Währungen so zu implementieren,
dass man die Kindobjekte miteinander vergleichen kann. Banane = Banane, orange != orange.

--- 
Der erste Teil ist scheinbar nur ein Praxisbeispiel.
Der Author geht noch ne ganze weile in die Richtung und zeigt TDD aus der Perspektive des Programmierers.
--- 


### Retrospektive
Das gezeigte Praxisbeispiel ist nicht fertig geworden. Es soll aber auch nicht fertig sein,
um zu demonstrieren, dass TDD auch nur eine Methode und ein Leitfaden und Kein Heilsversprechen ist.
Beck geht ebenfalls davon aus, dass man weitere Möglichkeiten nutzt, seinen Code automatisch reviewen zu lassen,
das vereinfacht das Refaktorieren später.

#### Code Metriken
Eine hier wirklich Interessante Metrik ist die zyklomatische Komplexität. Sie gibt an, wie viele Branches,
nestings und Loops im Code zu finden sind. Der Author hat allerdings getrickst, indem er das Typensystem und
eine menge Polymorphie genutzt hat (was meines wissens manchmal zu wesentlich Komplexeren Lösungen führen kann).

#### Test Qualität
3 arten von Tests können NICHT durch Unittests ersetzt werden:
- Performance
- Stress (Load Balancing etc.)
- Usability

Es gibt ein paar Metriken die außerdem noch Interessant sind:
- Statement Coverage (Wie viele Anweisungen wurden nicht mit einem Test gedeckt)
- Defekt Einsetzung (Ein extra falsch implementierter Code MUSS den Test brechen)

## The xUnit example
Das Ziel des xunit Examples ist es einen Überblick über unit Testing Frameworks zu geben,
etwas unter die Haube zu gehen und das ganze in python zu zeigen.

Das erste Ziel ist es Test Methoden evaluieren zu können. Dabei geht ein testing Framework eigentlich immer gleich vor:

- Global:
	- Setup All (Findet vor der ersten Methode statt)
- Einzelne Methode:
	- Setup each (Findet vor jeder Methode statt)
	- method (die zu testende Methode
	- teardown each (Findet nach jeder Methode statt)
- Global:
	- Teardown all (Findet nach der letzten Methode statt)


Die Idee ist eigentlich ziemlich einfach. Es wird ein Testobjekt erstellt, welches den Namen der Testmethode erhält.
Das Objekt kann anschließend aussagen, ob der Test stattgefunden hat oder nicht und den Test laufen lassen.
Das Ergebnis wird dann hinterher in den StdOut gepackt.

Das Objekt für den Testwrapper bekommt eine run methode, die die methode über reflection ausführt.
Das ganze wird dann als Programm (geht ja über die Kommandozeile) automatisiert.

Der Ablauf eines Tests besteht eigentlich immer aus 3 Stufen:
- Arrange (Objekte werden erstellt)
- Act (Führe den Test aus)
- Assert (Evaluiere das Ergebnis)

Beim Erstellen des Setup Methoden haben wir prinzipiell einen Interessenkonflikt.
Auf der einen Seite wollen wir geteilte Objekte haben, sodass jeder Test darauf zugreifen kann.
Das bringt performance. Auf der anderen Seite wollen wir das aber auf gar keinen Fall,
da sonst die Werte mutieren.

Beck geht erstmal mit dem Ansatz, dass erstmal nichts mutiert wird. So behalten die Tests ihre Integrität.
Es wird ebenfalls ein Schalter eingeführt, der überprüfen kann, ob das Setup einer Klasse bereits gelaufen ist.
Auch hier scheint der Author über reflection arbeiten zu wollen.

Beim Teardown macht Beck genau das gleiche. Um es noch besser visualisieren zu können, baut er für die Testsuite ein Log auf,
sodass jedes Setup und jedes teardown auch im log eingetragen wird. 
Danach implementiert Beck ein Counting System, um die durchgelaufenen Methoden zu zählen und über Erfolg und Misserfolg informieren zu können.
( 5 run, 2 Failed)

## Patterns for TDD

### Isolierte Tests
Es ist im prinzip ganz einfach: Wenn ein Test kaputt ist, soll auch nur eine Sache Kaputt sein.
Wenn 2 Tests kaputt sind, sollen 2 Sachen kaputt sein. Wenn Test voneinander isoliert sind und atomar nur
eine Funktionalität testen, können Fehler wesentlich früher erkannt und behoben werden.

### Jetzt oder Später?
Es kann immer sein, dass mir etwas beim Entwicklen auffällt oder zwischendrin in der "tiefen" Arbeitsphase etwas passiert.
Das muss verhindert werden, indem 2 Notitzen geführt werden. Notitzen für das jetzt also vllt für die nächsten 2,3 Stunden 
und Notitzen für später ( der große Plan) 

### Teste zuerst
Die Vorteile liegen vor allem in der Sicherheit und scope Dokumentation. Man weiß dadurch genau
was das System kann und wie es zusammengesetzt ist.

### Zuweisung zuerst
Das ist wie bei einer Mehtode/Function, wenn man den return wert zuerst beschreibt.
Man hat da den Vorteil, dass man direkt sich darum Gedanken macht, wie man das ganze mathematisch überprüfen soll.

### Testdatensätze
Es gibt unterschiedliche Testdatensätze. Das eine ist eine Art "Gerüst" für den Unittest.
Damit kann man schnell z.B über Mocks die Funktionalität beweisen. Das, was aber für "echtheit" sorgt,
ist es einen realistischen Testfall aufzubauen, mit echten Testdaten, unterschiedlichen Längen und Eingaben.

### Beweisdaten
Der Author schlägt vor sich selbst die Argumentation der Testfälle nachzuweisen,
indem man den Test so baut, dass man den Mathematischen Beweis als dritter oder man selbst(in 10 jahren ...) gut nachvollziehen kann.

## Red Bar Patterns

### One step 
Der Author schlägt vor stets von "Knowing" zu "Unknowing" zu gehen. Damit wird klar, was bewusst ist.
Ich mache das ja schon automatisch, wenn ich weiß "achja funktion X hat besonders viel Funktionalität, also drücke ich mich davor". 

### Starter Tests
Schreibe Tests, die den schnellen Pfad zum Fehlschag garantieren zuerst. Bevor ich also die ganze Funktionalität implementiere kann ich genau so gut mit einem Nulltest anfangen oder mal bei Integern 0 abtesten. Somit mache ich mir zuerst über ein und Ausgabe Gedanken.

### Explanation tests
Schreibe Tests, die den Zusammenhang zwischen Eingabe und Ausgabe erkären.
"Wenn ich Objekt X übergebe, und Einstellung XYZ getroffen wird, dann soll das Ergebnis so aussehen."

### Learning Tests
Beck schlägt vor wenn ich z.B eine Api Integriere ( Also third party services lohnen sich da wirklich für),
sollte man vielleicht die Api mal über die Testsuite ausprobieren. Dadurch kann man A) feststellen ob die Api funktioniert und B) Wie die Api zu benutzen ist. Das ist auch eine gute Art der Dokumentation

### Another Test
Kurzum: Neue Ideen sind wertvoll, allerdings nicht immer direkt verfolgenswert. Schreibs erstmal auf und mach weiter mit dem,
was du eigentlich wolltest.

### Regression Test
Dein Code ist Kaputt oder dir ist ein Defekt gemeldet worden? Dann musst du den Fehler Isolieren,
die Bedingungen durch Code darstellen in einem Test, der die genauen Bedingungen einfängt und dann den Bug beheben.
Erst so kannst du sicher sein, dass der Fehler auch wirklich weg ist. Wichtig hierbei ist, dass möglichst vollständige Informationen über die Betätigungen des Nutzers Informationen gesammelt werden (Log, GuiRecorder? )

### Mach eine Pause
Selbsterklärend. Der Author erwähnt noch, dass der auch länger gilt. Auch am WE mal was anderes zu machen, ist Gold Wert.

### Und nochmal!
Ne ernsthaft, wenn man nicht weiterkommt, kann es helfen, das ganze nochmal zu machen.
Einfach z.B beim Pair Programming mal den Partner wechseln oder oder oder....

### Investiere in einen guten Bürostuhl und dergleichen
Denn niemand kann gut programmieren, wenn sein Rücken wehtut. Außerdem
seh zu, dass du ne gute Tastatur hast und generell gute Hardware.

## Testing Patterns

### Child Test
Wenn der eigentliche Test zu groß ist, solltest du vielleicht 3 kleine draus machen.
Eventuell den großen als Integrationstest laufen lassen.

### Mocks
Mocks an sich sind schon n echt komplexes thema. Jedes mal, wenn ich eine starke Abhängigkeit habe, sollte ich vielleicht dran denken nen mock zu benutzen.
Das hab ich z.B im Hexenhammer schon gelernt. Einige Sachen werden einfach testbarer, wenn ich sie emuliere mit Mocks.
(Außerdem habe ich so auch keine gemeinsamen Objekte und die Tests sind voneinander losgelöst)

### Self Shunt
Muss ich ehrlich sein, das habe ich nur marginal verstanden. Das was ich verstanden habe ist auf jeden fall, dass der
Author empfiehlt, dass wenn ich z.B inferfaces teste, dass der Testcase sie selbst implementieren soll.

### Log Strings
Wenn ich z.B Asynchrones Verhalten implementiere also wenn ich was mit reaktiver Programmierung mache (Pub sub und so)
dann kann ich sowieso am besten alles loggen. Also kann ich ja auch abtesten, welche logs wann geschmissen werden.

### Crash Test Dummy
Hast du dich schonmal gefragt wie man die bazillionen Catches in Java eigentlich abtesten kann?
Die Antwort ist n einfacher crash test dummy, der garantiert eine Exception schmeißt.
Also wenn du n mock objekt anlegst oder so und z.B Testen willst wie sich das System verhält wenn die 
Festplatte voll ist kannst du doch eine der methoden einfach mal garantiert ne exception werfen lassen.
((DAS IST SUUUUUPER GUT, SO KANN MAN DAS SYSTEM KNALLHART UND RESILIENT MACHEN!!!))

### Clean Check in
Bevor du den code committest: lass die tests nochmal durchlaufen und mach alles sauber und update deinen code nochmal.

### Wo hab ich nochmal aufgehört?
Wenn du den Arbeitsplatz verlässt, dann lass den letzten Test kaputt oder zumindest das, woran du grad arbeitest. 
So weißt du ganz genau was du getestet hast und was du noch machen musst. (mach das aber um gottes willen nur lokal bei dir, sodass der
nächste keinen kaputten code bekommt)

## Green bar patterns

### Fake it till you make it
Der Author schlägt vor erstmal überall konstanten zu nehmen und dann die Konstanten auszutauschen "on the fly"
also etwas implementieren mit ner konstante und sobald ich da nen anderen wert brauche, weil sich der testfall oder die anforderungen ändern tausche ich das
ganze einfach aus.

### Triangulation
Ich bestimme das Verhalten des interfaces und Leite daraus die Implementierung ab. Also stelle ich mehrere Testfälle auf und sag "so und so muss sich der code verhalten".
Wenn ich z.B 2 unterschiedliche Tests habe für eine klasse "Plus" Ja das Beispiel ist echt zu einfach... Und ich dann 2 Testfälle habe,
dann kann ich daraus ableiten wie die Implementierung aussehen soll (Okay is total quatschig bei komplexeren geschichten) aber nevertheless kann ich 
immer wieder zuerst das Interface definieren und dann das Verhalten darunter implementieren.

## xUnit patterns

### Assertion
Alle Assertions evaluieren einen Boolschen Wert. Es gibt spezifische Methoden in einigen der Frameworks,
sodass asssert True nicht abused werden muss. Also sowas wie assertEquals oder assertSame.

#### Assert Equals
Vor allem für Mathematische Operationen geeignet assertEquals(50, result)
(erwarteterWert, ergebnis)

#### Assert Same
Vor allem für Objekte geeignet, (also da wird auch die Tiefe überprüft)
Also kann man sowas machen assertSame(object1, object2);

#### Conventions mit Fehlernachricht
Viele Teams haben Konventionen, sodass eine Nachricht hinterlassen werden muss im Assert True oder generell allem,
was einen Optionalen String als Parameter angibt. Warum? Damit man mehr Aussage über die Qualität des Werts bekommt, wenn doch noch
was schiefgeht

### Fixture
es ist üblich in einer Setup methode den gemeinsamen Testcase zu beschreiben. Das macht man normalerweise in der @BeforeEach.
- Auch ist es üblich in einem Teardown eine Datei zu schließen, wenn man sie in einem Test aufmacht (Also cleanup)

### Test Methoden
Die Mehtoden trennen durch Benennung den weizen von der Spreu. Wenn man eine halbwegs intelligente benennung der Testmethoden vornimmt, kann
man durch den methodennamen schon aussagen, was erfolg oder misserfolg über den Code aussagt. Außerdem kann man dadurch feature dokumentation betreiben.

### Exceptions testen
Das einfachste ist es hierbei einfach den Code zu callen der werden soll. Gestalte den Testcode so, 
dass er auf jeden fall wirft. Wenn die Exception nicht geworfen wird, hänge ein fail() hinter deinen Code im Test.
So kannst du sicherstellen, dass der Test nur durchläuft wenn A) Dein geschriebener Code die exception wirft und B) Kann es nur funktionieren, 
wenn die exception korrekt gehandhabt wird.

## Design Patterns
Die meisten Probleme die wir lösen, werden durch die tools verursacht die wir benutzen.
OOP dient genau diese Probleme herunterzubrechen. Design Patterns sind eine Sammlung genau dieser häufigen Probleme

### Command 
Eine Berechnung oder ein Stück code, dass einfach ausgeführt werden soll (side effect meist)

Is mehr so ne reactive programming Sache. Wir haben bei IKOffice z.B auch ne Client Server architektur, die sich aus einer Codebase ergibt. Da machen commands sinn, weil der client jederzeit command objekte erstellen kann und die zum server schicken kann.

Das Java Runnable interface ist da das beste Beispiel.

### Value Objekt 
Ein Objekt, dass lediglich Werte enthält.
BONUS: Wenn es immutable ist. Also z.B Records in Java. So kann ich Kompositionen mit Value Objekten schaffen, die mir alle nicht auf die Füße fallen.

### Null Objects
Der Name ist Irreführend. Der Author schlägt vor, statt überall Nullchecks einzubauen, einen Basecase einzuführen. Beck meint im Kontext von einem Rechtesystem z.B wäre es besser ein Default Objekt zu erschaffen, wo schon einige Infos drin sind, allerdings hald keine Nullen, damit das System weiterarbeiten kann und trotzdem klar is"hey das ding hier is noch nicht gesetzt"

### Template method
Eine Methode, die in einer Elternklasse aufgebaut wird und dann für die Kindklasse abgeleitet wird.

### Pluggable Object
im Prinzip Polymorphie der Objekte

### Pluggable Selector 
Im Prinzip meint der Author hier eine Kontrollstruktur wie einen Switch, der von außen z.B durch Construktor Injection gefüttert wird, und den weiteren Kontrollfluss bestimmt.

### Factory Method
Eine methode um Objekte drucken zu können.

### Imposter 
Eine neue Implementierung, die der Schnittstelle angepasst ist

### Composite
Ein Objekt, welches Verhalten einer bestimmten Gruppe von Objekten beschreibt.

## Refactoring

### Erkenne Unterschiede
Wenn es darum geht 2 identische Codestücke (identisch im sinne vom Gleicher Auftrag, sehr ähnlich)
dann bring die beiden nah aneinander. Woran unterscheiden Sie sich? Gib ihnen eine Gemeinsame Methode und versuch die Ausprägungen durch das Typensystem darzustellen.

### Isoliere Änderungen
Wenn ich ein großes Stück Code ändern will, sollte ich mir den Part zuerst heraussuchen, der verantwortlich ist für das was ich haben will. Dann extrahiere ich z.B eine eigene Methode daraus und benenne die Methode nach dem Schematischen Schnitt den ich gemacht hab. (Meistens is die methode dann privat)

### Migrate Data
Muss ich ehrlich sein, hab ich nicht ganz verstanden, warum das sinnvoll ist.
Ich mein Beck beschreibt ja wenn ich z.B eine Datenstruktur von einem einfachen Objekt auf Liste ändern will, dann sollte ich beide Implementierungen erst mitnehmen und dann die alte löschen aber mir fällt einfach kein Anwendungsfall an, andem das erwähnenswert wäre.

### Extract method
Große Methoden aufsplitten. Es geht darum grade große Kandidaten (wie z.B einer der alten revisionen des Hexenhammers) die Komplexität durch sinnvolles divide and conquer zu verringern.
Absolut notwending.

### Inline Method
Eine OOP Methode reconsidern. Also grade WEM oder welcher Entity die Methode gehört wird hier considered.

### Extract Interface
Wird vor allem Genutzt, um wie vorhin erwähnt code duplikate zu vermeiden und nur die unterschiede zu betonen.

### Method Object
Wie kann mein eine Komplizierte Berechnung am besten darstellen?
Mach ne klasse draus! Die Abhängigkeiten werden so zu parametern.
Mach wie bei der Runnable ne "handle" methode also sowas wie run(), damit 
der Nutzer dann auch hinterher was damit anfangen kann und starte da die berechnung und splitte die ganze methode angenehm weiter auf.

## TDD meistern
Erstmal kleine Schritte. Führt am ehesten zum Erfolg und Üben, Üben, Üben.
Nutze die Features deiner IDE und lerne deinen Editor. So kannst ich die refacotrings fast im Schlaf anwenden und es sind dann keine großen Umbauten sondern "zack zack alles".

### Wie weiß ich denn wie ich gute Tests habe
na wie sehen denn schlechte tests aus?
- Viel zu lange Setups
- Setup Duplikate (Jede methode setzt das gleiche auf)
- Tests die viel zu lange dauern, als das man sie laufen lässt
- Tests die einmal Funktionieren (ohne Änderunge) und dann wieder nicht

### Wie führt TDD zu bestimmten Frameworks
Wenn du anfängst Dinge zu abstrahieren. Wenn du deine Designs revisitest, passiert das automatisch.

### Wie viele Tests muss ich denn schreiben?
Wie gering ist deine mean time between failure? Also wie hart ist bei dir die Hütte am brennen, wenn der Code nicht funktioniert und eine failure verursacht und wann kommt der nächste Fehler?

### Wann sollten tests gelöscht werden?
Wenn es wirklich straight up duplikate sind mit gleichen Eingabe und Ausgabeparametern und vor allem, wenn sie innerhalb der gleichen Äquivalenzklasse den gleichen Pfad testen.

### Wie beeinflusst die Programmiersprache und die IDE den Workflow
Ja. Ich hab ja schonmal n paarmal scheme in nem plain editor geschrieben. Das sind welten unterschied.
Also schau, dass deine Entwicklungsumgebung (Egal ob plain Editor oder IDE) einfach die bestmöglichsten Tools hat für deinen Workflow.

### Kann man TDD durchführen mit RIESIGEN Systemen?
Ja. Separiere einfach die Integrationstests (am besten eigener Testserver) von den Unittests (Lokal) und du bist pfeilschnell unterwegs.

### Kann man TDD auch mit Acceptance Tests machen?
Nur wenn den Kunde onsite ist, sonst macht das keinen Sinn.
Du brauchst zur abnahme ja den Kunden.

### Kann man Mittendrin in nem Legacysystem anfangen mit TDD?
Ja aber mach das erstmal nur bei neuen Features only. Man kann schritt für schritt den alten Service immernoch refaktorieren, aber das macht keinen Sinn direkt alles umzukrempeln.


