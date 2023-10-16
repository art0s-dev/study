# Software Design und Architektur 
Diese Notitzen beziehen sich auf John Ousterhout's "principles of software Design"
Als Praxisprojekt um gelerntes umzusetzen wähle ich mein Hobbyprojekt Hexernhammer für
das Tabletopspiel Warhammer 40K. 

## Zum Vorwort
Es gibt für Softwaredesign mehrere "Ideen" aber keinen einheitlichen Standart.
Der Author schildert einfach seine Meinung, seine Erfahrung. Seine Ideen sind 
quasi "Battle tested". Das oberste Ziel des Buches und der Vorschläge 
ist die Reduktion vom Komplexität in Softwaresystemen.

## Einführung 
Bei der Entwicklung von Software geht es darum Gedanken strukturiert und
geordnet auszudrücken. Je älter eine Software wird, desto komplexer wird sie.
Wenn man die Zusammenhänge einer komplexen Software einfach ausdrücken kann,
ist sie verständlich. Im wesentlichen gibt es 2 Stragegien für die Bekämpfung von
Komplexität:
- Bekämpfung (durch Benennung, Dokumentation, Kommentare, Intention ausdrücken)
- Modularisierung (Die Komplexität wird in Module unterteilt, welche sich um verschiedene Teilaspekte kümmert)

Softwaredesign unterscheidet sich von Architektur, indem es nicht einmal geplant ist und dann fertig ist,
sondern es wird stetig daran gearbeitet. Jede neue "Runde" wird sich um Sauberkeit und Verbesserung gekümmert (sowohl für den
Kunden als auch für den Entwickler etc.. ). Wir rechnen im Lebenslauf einer Software damit, dass
sie öfter umgestaltet und umgeschubst wird, als uns lieb ist. Das macht jedes design besser.

Wir wissen, dass eine Mücke zum Elefanten wird. Wenn ich einmal Warnzeichen für
Komplexität anfange zu ignorieren, öffne ich der Komplexität Tür und Tor.
Wenn ich so ein Warnzeichen wahrnehme, sollte ich Schritte einleiten, um die Komplexität zu verringern.

## Komplexität - Was ist das eigentlich?
Es ist einfacher ein einfaches Design zu erkennen als eines zu erstellen. Komplexität ist alles,
was ein System schwer verständlich und schwer anpassbar macht. Komplexität ist eher beim Lesen als beim Schreiben zu erkennen.
Allgemein gibt es 3 Ausprägungen von Komplexität.

### Ausweitung von Änderungen
AKA: Wenn ich an einer Stelle drehe, muss ich auch an der anderen Stelle drehen
Stell dir vor du hast 3 Webseiten, alle haben den selben rotton. 
Und jede Webseite definiert den Rotton selbst - Macht es nicht Sinn dafür eine Konfig anzulegen?

### Kognitive Last
- Wie viel muss ich wissen, damit ich diesen Code schreiben kann? und woran muss ich noch denken?
Sowas passiert, wenn man viele Globale Variablen, Inkonsitenzen, Abhängigkeiten, schwierige Domäne etc. hat.
Auch Code hat beim Lesen eine Kognitive Last. Erinnest du dich an den manuellen Patchversuch bei DWM? Einbuchstaben Variablen
und generell Code der versucht "schlau" zu sein erhöht die Kognitive Last. Ebenfalls Code der obszön Verbos ist (Signal to Noise ratio) erhöht die kognitive Last.

### Unknown unkowns
AKA Die Wissenslücke. Code wird dann erst so richtig komplex, wenn es Dinge gibt, die ich nicht wissen kann.
(Weil sie nur der Senior weiß oder derjenige, der zuletzt dran gearbeitet hat, generelle Dokumentation fehlt
und man kann sich die Funktionalität nicht erschließen. 

>Ein einfaches System wäre also, wenn man das Gegenteil nimmt
>ein System, welches einfach zentral verwaltbar wäre (keine Spaghettis!),
>ein System, welches Abhängigkeiten, Intention klar kommuniziert (gerne mehr Zeilen, wenn Sie kein Sprachdurchfall sind),
>ein System, welches gut Dokumentiert und _offensichtlich_ ist.

