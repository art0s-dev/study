#Test Driven Development

Diese Notitzen beziehen sich auf das gleichnamige Buch von Kent Beck. Die Praxisübungen aus dem Buch werde ich
in hexenhammer's testsuite anwenden.


## Zum Vorwort

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

## Notitzen zum Geldproblem

Der Author will wirklich, dass man in den Tests, ein möglichst gutes Interface designed.
Der Vorschlag ist es sich wirklich von Test zu Test zu hangeln und sich auch gerne für den Arbeitsprozess
Notitzen zu machen, denn eins nach dem Anderen wird implementiert.

Im Refactoring Step geht es darum Duplikate zu entfernen, aber eigentlich
sind die Duplikate nur ein Symptom. Nehmen wir als Beispiel spezifischen Cod, der Abhängigkeiten erzeugt,
schlechtes Design und leaky abstractions (5 stellen müssen ein Verhalten implementieren statt nur einer Stelle.)
Der Author bedient sich beim Refactoring stark am "klassischen" Klassenaufbau und klassischer OO.


## Degenerate Objects

Der Author bezieht sich auf die 3 Stufen des Testens: 
- Ein gutes Interface
- Eine schnelle Lösung (schreib dir die gute Lösung auf, mach aber die schnelle)
- Implementier die gute Lösung statt des Provisoriums

Beck schlägt vor, dass es okay ist auch mal bestehende Tests zu überdenken oder zu ändern.
Man kann ja nicht immer nen guten Tag haben und mit "gutem" Design richtig liegen.

Es ist ebenfalls möglich um einen Test grün zu bekommen, Werte mit Konstanten zu belegen, statt der eigentlichen Implementierung,
WENN es hinterher durch die Implementierung ausgetauscht wird. So wird man flexibler.
Der Vorteil liegt darin, dass man so viel eher ein Gespür dafür bekommt, wie sich das System verhalten soll.

## Equality for all
Anbei Value Objekte Sind ein Pattern, allerdings haben sie eine Bedingung. Sie müssen immutable sein.

>Wenn man in Java Objekte vergleichen will muss man equals und hash code
>als methode implementieren




