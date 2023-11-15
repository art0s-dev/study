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


