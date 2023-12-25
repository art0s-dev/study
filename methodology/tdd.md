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

  

