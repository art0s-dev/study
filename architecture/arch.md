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

## Ursachen für Komplexität
Unter anderem kann man Abhängigkeiten als einer der Ursachen für Komplexität zählen.
Ganz vermeiden lassen sie sich nicht, aber ausdünnen. In der Regel hat man 2 Seiten der Abhängigkeit.
Einen Sender und einen Empfänger. Beispiel Webseite: Irgendwo muss eine Klasse definiert werden,
die den Rotton für alle Webseiten beinhaltet und sie per api zur vfg stellt.
Man kann den Compiler und das Typensystem dazu nutzen, solche Abhängigkeiten über das Typensystem zu vermerken.

Ein weiterer Grund kann unklarheit sein. Unklarheit im Sinne von Ausdruck.
In der Regel ensteht unklarheit dadurch, dass die Intention des Authors nicht
ausreichend kommuniziert wird und durch mangelnde Dokumentation.
Dokumentation ist allerdings nur der Nötige Füllwert.

Stellen wir uns also eine Flasche vor. Diese Flasche muss am Ende des Tages gefüllt sein.
Wenn wir eine gute Architektur haben, ist die Flasche gut mit wasser gefüllt. Der Rest wird gefüllt durch
Dokumentation. Wenn wir ein unklares und komplexes System haben, bekommen wir weniger wasser und der aufgefüllte Dokumentationsanteil
wird größer. 

Komplexität ist kein Feind, der einmal bekämpft werden muss und dann besiegt ist.
Komplexität muss jeden Tag aufs neue bekämpft werden. Jede Designentscheidung muss dazu beitragen, das
System ein kleines Stückchen einfacher zu machen.

## Strategische und Taktische Programmierung (Makro vs Mikro)
Taktische Programmierung ist eine kurzfristig gesehene Planung. Ofmals wird in Unternehmen taktisch Programmiert,
um schnell von einem Feature zum nächsten zu kommen und damit wird keine Zeit für Designentscheidungen und dem
Bekämpfen der komplexität gewidmet. Die taktische Programmierung zeichnet sich aus als der kürzeste Weg
zu einem momentanen Erfolg. In jedem Team gibt es mindestens eine Person, die taktisch Programmiert.
Diese werden natürlich von den Leuten gefeiert, die bspw. in PO Position sitzen, hinterlassen aber meistens
eine Schneise der Verwüstung.

Bei der Stategischen Programmierung ist es (neben den funktionalen Anforderungen) eine gute Architektur und einen guten Lösungsweg zu finden,
der simpel und verständlich ist. (also gut Wartbar). Wie in dem Talk von Robert Martin wissen wir ja,
dass wenn man länger an einem Projekt sitzt und man nur die ganze Zeit taktisch programmiert, dass dann die Produktivität abnimmt.
Und genau das verhindert die Startegische Programmierung. 

Bei der strategischen Programmierung geht es (wir wissen, dass alle wege nach rom führen), um Optionen. 
Es gibt immer mehrere Wege etwas zu tun aber welcher ist tatsächlich auch der nachhaltigste?
Damit wir allerdings die Produktivität nicht vernachlässigen wäre eine Spanne von etwa 20% angemessen.
Also von 8 Stunden Arbeit - 1,5 Stunden. Es geht nicht darum jeden Tag eine Bärenladung zu schaffen, sondern
einfach darum jeden Tag ein bisschen zu machen. (Natürlich gibt es größere Brocken und kleinere Brocken - das ganze muss nochmal weiter aufgeteilt werden. Aber wann lohnt sich das alles? Kurzum: Wenn ich vor habe das Projekt langfristig zu betreuen.

## Von der Wahrheit
Wir wissen: wenn wir einmal anfangen mit dem Kurs "taktisch", muss die Umkehr vom Kurs genau berechnet werden.
Wie viel kostet es alles neu zu schreiben vs wie viel kostet das aufräumen vs wie viel kostet es, alles zu lassen wie es ist?

Aber: taktisch geht schneller; erzeugt aber technische Schuld. Facebook hat das z.B gemacht. Zwar befähigt das Leute 
ungemein und die Lernkurve wird auch eine immer bessere, aber selbst FB haben hinterher ihr Motto geändert.
Eine starke technische Kultur, die Lösungsorientiert arbeitet ist der Schlüssel zum langfristigen Erfolg.

## Modulares Design
Das beste was passieren kann, ist das Module vollkommen losgelöst voneinander bearbeitet werden können.
Somit würde die Software nur so komplex sein, wie das schlimmste Modul. Ist leider nur unrealisitisch.
Module MÜSSEN zusammenarbeiten. Also ist es das Ziel die Abhängigkeiten zwischen Modulen zu verringern.
Jedes Modul besteht aus Interface und Implementierung. Hier gilt das Eisbergprinzip. Kleine Spitze ist
das Interface und der eigentliche Eisberg ist die Implementierung. Das soll es einfach machen, damit zu arbeiten.
Klassen können in objektorientierten Sprachen als Module eingesetzt werden.

Jede Schnittstelle hat 2 Arten von Informationen. Formelle und informelle.
Formelle sind Übergabewerte und Rückgabeparameter. Informelle sind sowas wie spracheneigenes Verhalten.
Also Dinge, die erstmal garnicht so offensichtlich sind. Es wäre also logisch alle Informationen 
zur Entwicklung mit Methode X in die Schnittstelle zu legen. Dazu eignen sich z.B ja Interfaces.
Da lese ich keine Implementierung, sondern habe nur eine High-level übersicht, was das eigentlich macht.

## Abstraktionen
Abstraktionen sind vereinfachte Darstellungen einer Idee.
Jedes Modul sollte eine Schnittstelle in Form einer Abstraktion bereitstellen. Je mehr unwichtiger Krams weggelassen wird,
desto besser ist die Abstraktion.Eine Abstraktion die wichtige Informationen weglässt oder unwichtige Informationen beinhaltet
ist grundsätzlich fehlerhaft. Jedes mal, wenn ich etwas tun kann, ohne zu verstehen was unter der Haube ist,
hat die Abstraktion mir Zeit erspart. 

## Natur der Module
Es gibt Tiefe und Flache Module. Fangen wir einfach mit den tiefen Modulen an.
Ein "tiefes" Modul hat viel viel viel Funktionalität inne, bieter aber zugleich eine minimale Schnittstelle mit nur wenigen
Methoden. So ist es einfach das ganze zu begreifen. Wir bevorzugen immer Tiefe Module.
Als beispiel wird die IO Schnittstelle von Unix angeführt. Die benutzten functions sind open, close, read, write, lseek.
5 Methoden für massive Funktionalität - hier wieder: das Eisbergprinzip.

Ein weiteres Beispiel für gute Modularisierung ist z.B die GC in Java. Die braucht garkeine Schnittstelle und arbeitet im Hintergrund.
Flache Module sind Module, die viel Schnittstelle bieten und wenig Implementierung dahinter. Sie sind nicht immer vermeidbar,
jedoch sind sie ein Warnzeichen für Komplexität.

Der Author erwähnt hier noch in einem Abschnitt, dass Ideen wie Klassen dürfen nicht länger als X sein
oder eine Methode darf nur 6 Zeilen haben für unsinnig, da sie automatisch zu vielen kleinen flachen Klassen führe.
Brian Will hat sowas als "lost surface" beschrieben, als sei der Code eines Moduls ein Marmorblock.
Wenn ich den Marmorblock zerschlage splittert die Komplexität überall hin.

Als negativbeispiel wird die Java I/O genannt. Es müssen unsinnige buffered Objects erstellt werden, um schreiben und
lesen zu können. Da lässt der Author die Gegenthese Fallen
<b>Schnittstellen sollten so designed sein, dass sie den häufigsten Fall abdecken</b>

## Information Hiding
Es ist das Ziel eines Moduls die Internen Informationen der Implementierung und
die damit einhergehende Komplexität um jeden preis nach außen zu verbergen. Datenstrukturen sollten auch möglichst versteckt sein.
Wenn ein Modul keine Abhängigkeiten in der Schnittstelle kommuniziert, sollten keine Abhängigkeiten existieren - noch nicht mal Implizite.
Selbst wenn ich über getter und Settter eine Schnittstelle zur verfügung stelle, sind darudch private methoden und attribute 
immernoch sichtbar. Es wäre also logisch für die Sachen die ich verstecken will <b>KEINE</b> getter und setter anzulegen.

Es wäre ja eine gute Überlegung, dass wenn ich eine Datenstruktur nach außen Zeige, dass ich dann eine dedizierte simple methode zur Verfügung stelle,
damit von außen damit ohne Bedenken gearbeitet werden kann.

Das Gegenteil davon sind Informationslecks. Also wenn Informationen über Implementierung, generell das WIE nach außen bluten.
Das gilt auch wenn ich das gleiche Wissen auf meherere Klassen aufteile. Wenn ich z.B die gleiche oder Ähnliche Business logik,
die eigentlich zum gleichen Feature gehört in unterschiedlichen Klassen beschreibe, sollte ich mir überlegen das ganze vielleicht doch in
einer übergeordneten Klasse zusammenzufassen. Auch wenn die Methode/Klasse dann länger wird.

Module sollten also gebündelt werden und die Schnittstelle sollte so schmal wie möglich gehalten werden.
Der Author stellt weiterhin heraus, dass zeitliche Dekomposition zu vermeiden ist. Also wenn ich z.B eine Methode habe:
- tue dies 
- lese das
- werte das aus

Dann wäre ich gut beraten, das ganze nicht in 3 unterschiedliche Klassen zu verpacken, vielleicht noch nicht mal unterschiedliche methoden
(vielleicht eher methoden in der methode mit lambdas???? ), weil das die Schnittstelle gefährden kann und die Komplexität erhöht wird.
Der elementare Satz lautet hierbei "Was muss ich wissen, um diese Aufgabe zu erledigen?" Selbst Methoden die zu einem Anderen Zeitpunkt ablaufen (crons) oder generelle Asynchrone implementierungen können dem Modul hinzugefügt werden.

Das korelliert mit dem Single Responsibility Prinzip von Robert C Martin. Eine Klasse sollte nur eine Sache tun.
Wenn ich z.B ein Modul habe, dass HTTP Server heißt (Beispiel ausm Buch) wäre ich gut beraten alles was mit HTTP zu tun hat 
mit einer geschickten Schnittstelle alles in diese Klasse zu packen.
Und nochmal es springt mich fast schon förmlich an: Bitte keine Datenstrukturen nach außen entblößen.
Versuche eher Methoden zu schaffen mit der Datenstruktur zu arbeiten.

Versuche ebenfalls so viele default Werte wie möglich zu treffen. Parameter, die man sich schenken kann,
sind gute Parameter. Und weniger Informationen, die ich nach außen mitteilen muss. Ein Warnzeichen ist hier
wenn ich von einer Schnittstelle gezwungen werde, mit anderen Methoden zu arbeiten ist die Schnittstelle nicht gut.

Für Interne schnittstellen innerhalb einer Klasse: Wenn ich per getter mir die Abhängigkeiten eines Attributes ziehe
und ganz nach oben in die Methode packe und es als Dependency injection verkaufe hab ich besonders hart gefailed.
Weil dafür gibt es ja parameter und das ist implizite Konmplexität. Also: Stellen minimieren, wo ich auf instanzvariablen zugreife.

## Vielseitige Module
Spezialisierung führt zu Komplexität. Generalisierung zu guten Abstraktionen. Wenn ich mit einer Codierung, die 80% aller Fälle abdeckt 
arbeiten kann, ist sie gut. Eleminiere Sonderfälle durch die Schnittstelle und decke Randfälle möglichst automatisch ab.
Spezifische Implementierung muss in der Wartung oftmals wieder aufgeschnitten werden und erweitert werden.

Es gibt prinzipiell 2 Arten der Erweiterbarkeit und die zu unterscheiden braucht sehr sehr <b>sehr</b> viel Erfahrung. 
Die eine Art ist ein Gedanke ähnlich wie "INSERT BELL IQ CURVE MEME HERE" _nooo du musst unbedingt hexagonale architektur verwenden ... bla bla _
Das ist gefährlich und führt zu echten Overengenieering und das bringt nu wirklich keiner Sau was. Du wirst nicht fertig,
das Design ist scheiße und kein Mensch weiß, was du eigentlich willst und deine Kollegen hassen dich.

Die andere Art ist mehr so ein "ha, ich glaub der Kunde wird das sowieso ändern wollen" - Das ist oftmals der Gedanke, der dich 1,2 Functions mehr schreiben lässt.
Aber: Wenn aus der Erfahrung heraus gehandelt wird, kommt der Kunde oftmals wirklich an und wird die Funktionalität ändern lassen wollen.
Also bereitest du dich drauf vor, die Sachen etwas modularer anzugehen und dynamischer zu gestalten, damit du auf Änderungen der Anforderungen vorbereitet bist.
(Und was ist der Prozess der Softwareentwicklung eigentlich außer ein großes sich Ändern der Anforderungen!?!?!)

Erfahrungsgemäß ist generalisierter Code auch kürzer. Wenn ein Modul sich eher wie eine "Theke" verhält, ist es einfacher,
sich daran zu bedienen / bedienen zu lassen, da klarer ist, was bereitgestellt wird, statt dass man selber suchen muss.
Außerdem müssen so andere Entwickler nicht die ganzen edgecases lernen, sondern können stadtdessen mit einer angenehmen
80% Lösung arbeiten, wo man sich keine Implementierungsdetails merken muss.

>Die wichtigsten Fragen bei der Erschaffung generalisierter Schnittstellen lauten:
> - _Wie sieht die <b>einfachste</b> Schnittstelle aus, die meine aktuellen Bedürfnisse abdeckt?_
> - _In wie vielen Situationen wird diese Methode eingesetzt werden?_ 
> - _Kann man die Schnittstelle einfach verwenden?_

## Spezialisiserung nach Oben oder nach unten schieben
Spezialisierung ist in Softwaresystemen nicht vermeidbar. Oftmals zahlt der Kunde für spezialisierte Features.
Da habe ich prinzipiell 2 Optionen das ganze anzugehen. Ich gehe immer davon aus, dass die Anwendung einen generalisierten Kern hat.
Dieser Kern bietet eine einfache Schnittstelle für z.B das Gui. Wenn ich eine spezialisierte Lösung implementieren soll, muss ich schauen was besser passt:
ist das Feature Low level und der nächste Entwickler soll sich nicht mit Implementierungsdetails herumschlagen kann ich
den spezialsierten Code _nach unten schieben_ und unter der Abstraktion des Moduls den code verstecken.
Oder ich _schiebe den code nach oben_ und beschreibe z.B im Gui(oder in einer anderen Klasse..) das Feature und lasse den Kern
der Anwendung generalistisch.

Es ist ebenfalls möglich beides zu machen. Also Anwendungsregeln in einer generalisierten Klasse zu verfassen 
und die Umsetzung der Regeln in einem Spezialsiertem Submodul vorzunehmen (wobei man da auch auf diese Klassizites achten muss.. weniger ist da mehr )

## Verschiedene Schichten - Verschiedene Abstraktionen
Software ist eine Zwiebel Aus Theken. Jede Schicht bedient sich an der unteren. Je weiter nach unten es geht, desto "low leveliger" sollte es werden.
Also sollten sich die Oberen Schichten nicht mit Speicherkapazität oder Output Buffer befassen und die Unteren nicht Gui Logik - sollte eigentlich klar sein.

Gutes Anzeichen für unnötige Komplexität sich pass-thru methoden also Methoden die einfach nur andere Methoden aufrufen. Das ist ja gut und schön eigentlich,
nur wenn ich a) die methode nur an einer Stelle verwende kann ich sie auch ausschreiben und b) wenn die Methode Side effects hat, muss der nächste Entwickler anfagen das
alles nachzuvollziehen. Außerdem sorgen diese Art der Methoden dafür, dass refactoring die Hölle wird.

Das ganze lässt sich vermeiden, indem man die Methoden entweder direkt aufrufen kann oder den Callstack(wenn er nur einmal verwendet wird) hinter einer guten Api
in einer Klassse eindampft.

## Wann ist es OK dopplungen zu haben?
Bei Dispatchern ist das grundsätzlich erstmal OK. Ein dispatcher ist eine Methode, die als "controller" andere Methoden aufruft und Argumente weitergibt.
Dieser stellt im Gegensatz zu Pass thru methoden eigene Funktionalität zur Verfügung.
Ein Dispatcher wird z.B bei der Implementierung einer Api oftmals genutzt, um die unterschiedlichen HTTP Methoden anzusteuern.

Bei den Decorator Pattern ebenfalls. Das ist aber mehr so ein "it depends". Das Decorator Pattern ist ein Objekt, welches ein Objekt beinhaltet 
und on top eigene Funktionalität draufschlägt und dann die getter und setter des darunterliegenden Objekts nutzt. Das ist OK. Dabei sollte man
sich allerdings fragen:
- Wäre es nicht Sinnvoll diesen Fall in die darunterliegende Klasse einzubauen, um weiter zu generalisieren?
- Wird die Klasse für einen Speziellen Fall benötigt? Ist es nicht Sinniger das ganze eine Schicht höher z.B ins Gui zu ziehen?
- Könnte man einen bereits bestehenden Decorator Nutzen?
- Muss es als decorator laufen oder kann es auch als einzelne Komponentenklasse implementiert werden?

## Pass Thru Variablen
Wenn ein größeres System gewarter wird, neigt man oftmals dazu einfach die Parameterliste einer Methode zu erweitern
und dann dort die benötigte Funktionalität einzufädeln. Das bitte nicht tun, sondern mögliche einfachere alternativen zum Umgang 
mit Objekten nutzen. Ist ein DTO für die Parameter Sinnvoll? So haben wir nur einen Parameter, können die Liste verlängern
und das Feld, was wir hinzufügen möchten komplett Optional machen. Wird zwar nicht gerne gesehen aber es ist auch möglich
das gewünschte Feld als Globale Variable (scoped innerhalb der muttermethode) zur verfügung zu stellen.

## Komplexität nach unten ziehen
> Einfache Schnittstelle > einfache Implementierung. 
> Entweder ist die Komplexität in der Sprache oder in der Anwendung.

Alles was ich durch die Schnittstelle nach außen Kommuniziere, muss sich ein anderer in den Schädel hämmern.
Je Intuitiver ich die Schnittstelle gestalte, desto besser. Es ist möglich die Anwendung der Schnittstelle weiter zu verfeinern durch
Konfigurationsparameter. Allerdings führt jeder Parameter auch dazu, dass sich jemand den Mist merken muss.
Also wäre Ideal jeden Edgecase durch Konfigurationsparameter Abzufangen und einen Standartwert zu schaffen.
Also für den Fall, dass es doch jemand konfigurieren und verändern möchte (man es sich aber nicht merken muss (80 - 20 regel))

## Zusammen oder getrennt?
Es gibt 2 Worstcase Szenarien. 1) Die Gesamte Software befindet sich in einer Klasse. 2) Die Gesamte Software befindet sich in 627.844 Klassen
Wir merken also Komplexität steigt in der Implementierung mit der Tiefe der Klasse (wenige Klassen - kleine schnittstellen) und die Komplexität
steigt in der Anzahl der Schnittstellen. (Wilde Getter Setter, Pass thru methoden) Ebenfalls macht das Aufteilen einer Methode die Methode schwerer Lesbar.
Wenn ich eine Methode hab, die z.B in 5 kleinere Methoden unterteilt werden kann, sollte ich (wenn sie nur einmal verwendet werden) die methoden
möglichst beieinander lassen. Also nicht einen 50 Zeiler in 5 Klassen verteilen, nur damit es mehr nach "clean code" aussieht.

Also wäre es ja Sinnig Codeelemente zu gruppieren nach Zugehörigkeit. Wenn also gleiche Informationen genutzt werden sollen, 
oder die Schnittstelle sowieso sehr ähnlich ist, macht es ja durchaus sinn den Code zusammenzufassen. 

