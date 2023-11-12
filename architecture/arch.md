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

### Ursachen für Komplexität
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

### Von der Wahrheit
Wir wissen: wenn wir einmal anfangen mit dem Kurs "taktisch", muss die Umkehr vom Kurs genau berechnet werden.
Wie viel kostet es alles neu zu schreiben vs wie viel kostet das aufräumen vs wie viel kostet es, alles zu lassen wie es ist?

Aber: taktisch geht schneller; erzeugt aber technische Schuld. Facebook hat das z.B gemacht. Zwar befähigt das Leute 
ungemein und die Lernkurve wird auch eine immer bessere, aber selbst FB haben hinterher ihr Motto geändert.
Eine starke technische Kultur, die Lösungsorientiert arbeitet ist der Schlüssel zum langfristigen Erfolg.

### Modulares Design
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

### Natur der Module
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

### Information Hiding
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

### Vielseitige Module
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

### Spezialisiserung nach Oben oder nach unten schieben
Spezialisierung ist in Softwaresystemen nicht vermeidbar. Oftmals zahlt der Kunde für spezialisierte Features.
Da habe ich prinzipiell 2 Optionen das ganze anzugehen. Ich gehe immer davon aus, dass die Anwendung einen generalisierten Kern hat.
Dieser Kern bietet eine einfache Schnittstelle für z.B das Gui. Wenn ich eine spezialisierte Lösung implementieren soll, muss ich schauen was besser passt:
ist das Feature Low level und der nächste Entwickler soll sich nicht mit Implementierungsdetails herumschlagen kann ich
den spezialsierten Code _nach unten schieben_ und unter der Abstraktion des Moduls den code verstecken.
Oder ich _schiebe den code nach oben_ und beschreibe z.B im Gui(oder in einer anderen Klasse..) das Feature und lasse den Kern
der Anwendung generalistisch.

Es ist ebenfalls möglich beides zu machen. Also Anwendungsregeln in einer generalisierten Klasse zu verfassen 
und die Umsetzung der Regeln in einem Spezialsiertem Submodul vorzunehmen (wobei man da auch auf diese Klassizites achten muss.. weniger ist da mehr )

### Verschiedene Schichten - Verschiedene Abstraktionen
Software ist eine Zwiebel Aus Theken. Jede Schicht bedient sich an der unteren. Je weiter nach unten es geht, desto "low leveliger" sollte es werden.
Also sollten sich die Oberen Schichten nicht mit Speicherkapazität oder Output Buffer befassen und die Unteren nicht Gui Logik - sollte eigentlich klar sein.

Gutes Anzeichen für unnötige Komplexität sich pass-thru methoden also Methoden die einfach nur andere Methoden aufrufen. Das ist ja gut und schön eigentlich,
nur wenn ich a) die methode nur an einer Stelle verwende kann ich sie auch ausschreiben und b) wenn die Methode Side effects hat, muss der nächste Entwickler anfagen das
alles nachzuvollziehen. Außerdem sorgen diese Art der Methoden dafür, dass refactoring die Hölle wird.

Das ganze lässt sich vermeiden, indem man die Methoden entweder direkt aufrufen kann oder den Callstack(wenn er nur einmal verwendet wird) hinter einer guten Api
in einer Klassse eindampft.

### Wann ist es OK dopplungen zu haben?
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

### Pass Thru Variablen
Wenn ein größeres System gewarter wird, neigt man oftmals dazu einfach die Parameterliste einer Methode zu erweitern
und dann dort die benötigte Funktionalität einzufädeln. Das bitte nicht tun, sondern mögliche einfachere alternativen zum Umgang 
mit Objekten nutzen. Ist ein DTO für die Parameter Sinnvoll? So haben wir nur einen Parameter, können die Liste verlängern
und das Feld, was wir hinzufügen möchten komplett Optional machen. Wird zwar nicht gerne gesehen aber es ist auch möglich
das gewünschte Feld als Globale Variable (scoped innerhalb der muttermethode) zur verfügung zu stellen.

### Komplexität nach unten ziehen
> Einfache Schnittstelle > einfache Implementierung. 
> Entweder ist die Komplexität in der Sprache oder in der Anwendung.

Alles was ich durch die Schnittstelle nach außen Kommuniziere, muss sich ein anderer in den Schädel hämmern.
Je Intuitiver ich die Schnittstelle gestalte, desto besser. Es ist möglich die Anwendung der Schnittstelle weiter zu verfeinern durch
Konfigurationsparameter. Allerdings führt jeder Parameter auch dazu, dass sich jemand den Mist merken muss.
Also wäre Ideal jeden Edgecase durch Konfigurationsparameter Abzufangen und einen Standartwert zu schaffen.
Also für den Fall, dass es doch jemand konfigurieren und verändern möchte (man es sich aber nicht merken muss (80 - 20 regel))

### Zusammen oder getrennt?
Es gibt 2 Worstcase Szenarien. 1) Die Gesamte Software befindet sich in einer Klasse. 2) Die Gesamte Software befindet sich in 627.844 Klassen
Wir merken also Komplexität steigt in der Implementierung mit der Tiefe der Klasse (wenige Klassen - kleine schnittstellen) und die Komplexität
steigt in der Anzahl der Schnittstellen. (Wilde Getter Setter, Pass thru methoden) Ebenfalls macht das Aufteilen einer Methode die Methode schwerer Lesbar.
Wenn ich eine Methode hab, die z.B in 5 kleinere Methoden unterteilt werden kann, sollte ich (wenn sie nur einmal verwendet werden) die methoden
möglichst beieinander lassen. Also nicht einen 50 Zeiler in 5 Klassen verteilen, nur damit es mehr nach "clean code" aussieht.

Also wäre es ja Sinnig Codeelemente zu gruppieren nach Zugehörigkeit. Wenn also gleiche Informationen genutzt werden sollen, 
oder die Schnittstelle sowieso sehr ähnlich ist, macht es ja durchaus sinn den Code zusammenzufassen. 
Also Zusammenfassen, was zusammgengehört. Wenn Teile der Lösung in verschiedenen Klassen implementiert sind, 
ist es doch erstmal eine gute Idee das ganze zusammenzubringen, damit weniger Oberfläche und damit weniger Schnittstellen vorhanden sind.
Ebenfalls kann ich so wiederholungen vermeiden.

> Wenn ich mehrmals hintereinander den gleichen (oder sehr ähnlichen code) vorfinde
> habe ich noch nicht die richtige Abstraktion gefunden

Code der allgemein und vielfältig verwendbar ist und z.B Kontrollmechanismen enthält, sollte möglichst
von spezialisiertem Code (dem edgecase, der implementierung für x, den bugfix für y) getrennt sein.
Denn wenn ich beides zusammen lasse und wenn ich den allgemeinen code warten muss, muss ich jedes mall oder muss jeder der den code anfässt,
das ganze Gerüst verstehen. Das ist ja nicht Sinn der Sache. 

Doch wo verläuft da die Grenze? Nehmen wir mal das Beispiel, dass wir eine lange Methode behandeln wollen.
Sowas wie in meinem aktuellen Projekt Hexenhammer die Schadenskalkulation. Es ist im Prinzip eine Sequenz die behandelt wird,
welche zu einem Endergebnis führt. Also sollte diese Methode zusammen bleiben. Wenn ich allerdings darin Subroutinen sehe,
welche ich problemlos losgliedern kann (also auch durchs threading jagen kann), sollte ich diese ausgliedern.
Wenn die Methode allerdings zu viel auf einmal regelt (und zu viele Überraschungen parat hält, sowas wie side efects),
dann steigt die Komplexität und ich könnte passende Teile ausgliedern.

Das heißt es würde keinen Sinn machen, wenn eine Methode einfach zu behalten ist und einfach zu lesen ist, diese in
unterschiedliche Methoden zu verfrachten. Das würde A) die Oberfläche der Schnittstellen erhöhen und B) hat es das potential die Implementierung
noch komplexer zu machen. Also ist Methodenlänge kein Kriterium, sondern Komplexität.
ABER: Sagen wir ich habe 3 untermethoden. Wenn ich 2 und 3 nur verstehen kann, wenn ich 1 gelesen habe, sollte ich sie zusammenlassen.

<b>Jede Methode sollte eine Sache tun, diese aber vollständig</b>
Eine Idee wäre es nur Sachen auszulagern, die für Multithreading oder asynchrone Abläufe gebraucht werden. 
Der Meiste Code mit Multithreading sollte sowieso so gestrickt sein, dass ich feste variablen übergebe und 
der multithreading code so gut es geht keine Nebeneffekte beinhaltet.

## Ousterhout über clean code
Er stellt sich eher die Frage bei Uncle Bobs Regel, wie lang eine Function sein sollte, ob es Nützlich ist eine große Funktion zu haben oder viele kleine.
Er ist dabei der Meinung, dass mehr Schnittstellen(also mehr Methoden) auch zu mehr Komplexität führen, da mehr Schnittstellen überwacht und erlernt werden müssen.

## Die Existenz von Fehlern wegdefinieren
Oder: Wie wir Exceptions so verwenden können, dass Sie die Komplexität unserer Anwendung nicht erhöhen.
Exceptions sind per definition etwas, was nicht sein sollte. Sagen wir wir schreiben eine Datei. Das geht nicht weil Festplatte voll, zack Exception.
Exceptions erhöhen die Komplexität der Anwendung, weil sie den "normalen" Ablauf stören.
Grad in Java wird man als Programmierer dazu verpflichtet diese Ausnahmefälle zu behandeln. Prinzipiell gibt es 2 Wege wie man mit solchen Exceptions umgeht:
1) Man versucht den "Kaputten" Zustand zu bereinigen oder man versucht es nochmal (notfallplan umsetzen)
	- John erwähnt anbei, dass der so operierende Code auch exceptions wirft, was zusätzliche Komplexität bedeutet.
2) Man gibt den Fehler nach Oben an den Nutzer oder an weitere Module zurück (fliegen lassen)

><b>Code der nicht ausgeführt wurde, funktioniert nicht!</b>
>Also sparsam sein, mit Code zur vermeintlichen Fehlerbereinigung, da es hierbei oft zu vollkatastophen kommen kann

Die von einer Klasse geworfenen Exceptions sind Teil der Schnittstelle. Das heißt jede Exception erhöht die Komplexität meiner Schnittstelle.
Das heißt ich muss mir im Modul selber im besten Fall Gedanken machen, wie ich mit den aufkommenden Exceptions umgehen kann.
Der Autor stellt dafür 4 Techniken vor:

### Die Existenz selbst wegdefinieren
Also innerhalb des Moduls selbst das Problem lösen, sodass ich mich von außen nicht damit rumschlagen muss.
Als Beispiel wird das Datei löschen in Windows vs Linux angeführt. Bei Windows ist es nicht möglich eine Datei zu löschen, während sie verwendet wird.
Bei unixsystemen wird allerdings ein asynchroner prozess gerufen, der einen Buffer der Datei erstellt, sodass alle Prozesse, die aktuell darauf zugreifen noch
drauf zugreifen können. Für alle anderen gilt die Datei allerdings als gelöscht. Das Ergebnis ist, dass der Nutzer hier weniger entscheiden muss, sondern einfach
Löschen kann. Das reduziert den overhead.

Als weiteres Beispiel wird hier die Java Substring methode genannt. Die wirft eine Exception, wenn der Index nicht innerhalb des Strings verfügbar ist.
Also sagen wir ich hab ein "wort".substring(0,4) (mit indexzählung wären das 4 Buchstaben 0,1,2,3) Die 4 würde eine Exception verursachen.
Es wäre also einfacher ein leeres Ergebnis zurückzugeben, wenn sich der Index nicht im String befindet.

<b>Insgesamt reduziert man die Fehler einer Software, indem man sie EINFACHER!!!!! macht</b>

>Info: Ein Exception handler ist ein Stück code, welcher ausgeführt wird, wenn es zum Notfall kommt.
>Merke: Ein robustes System hat Pläne für solche Notfälle. (Sollte aber nicht zugekleistert werden mit defensiver Programmierung)
>Ich will ja immernoch den "normal case" ausdrücken können. 

### Exceptions maskieren
Das Maskieren von Exceptions ist sehr ähnlich, jedoch findet man hier als Beispiel asynchrone hintergrundprozesse.
Also wenn z.B in einer Anwendung die Konnektivität verloren geht, wäre es durchaus sinnvoll, den Fehler zu maskieren (keine Exception)
und solange zu warten, bis die Konnektivität wieder hergestellt ist. Das gleicht am ehesten dem Notfallplan, den ich oben erwähnt habe.
Das Funktioniert zwar nicht immer, aber ist durchaus möglich. Der Code sollte natürlich so gehalten werden, dass er keine weiteren Exceptions verursacht.
Also hier keine Experimente und was an den Datenstrukturen rumfuchteln, sondern einfach Warten und vllt nochmal versuchen.

<b>Wichtig</b>: Der Code zur Fehlerbehandlung wäre als eigene Exception angemessen und sollte von den anderen Exceptions klar getrennt sein.
Also vllt auch visuell hervorgehoben.

### Aggregieren von Exceptions
Also damit ist das Zusammenführen von Exceptions gemeint. Oder auch Bündeln. Wenn ich z.B eine Methode verwende, die eine Exception werfen kann, würde es ja Sinn machen
die Methode an nur einer Stelle zu rufen, das Ergebnis wegzuspeichern und dort einmal alle Exceptionhandler zu definieren. So müssen sich die anderen Module mit den Exceptions nicht auch noch rumschlagen.
An der Stelle wird also vorgeschlagen einen generalisierten Weg der Fehlerbehandlung zu gehen.
Also sagen wir mal wir haben ein Backup System aus mehreren Maschinen. Wenn eine Maschine ausfällt wegen
Fehler X sollte doch eher der Weg der Fehlerbehandlung sein: Egal was der Fehler ist,
starte eine weitere Virtuelle Maschine und binde Sie in z.B den Raid mit ein.
Dadurch habe ich einen gebündelten Weg der Fehlerbehebung unabhängig davon, was der Fehler ist.

### Einfach Crashen Lassen
In jeder Anwendung gibt es Fehler, die sich nicht lohnen sie zu fangen. Zum Bleistift wären das Out of Memory
Exceptions. Wenn es ein seltener Fall ist, der sehr unwahrscheinlich ist, würde es die Anwendung nur noch
komplexe machen, sich auch auf den Fall vorzubereiten. Vor allen Dingen, wenn der grade bearbeitete Workflow nicht Systemkritisch ist. 

### (5) Logging
Der Author geht darauf ein, dass man mit dem verschleiern der Fehlermeldungen zu weit gehen kann,
sodass dann die Anwendung schlechter Wartbar ist. Im allgemeinen Empfiehlt es sich
ordentlich die Anwendung zu Loggen, um den Weg des Fehlers nachvollziehen zu können.
So kann man also die Entscheidungen des Programms lesen und trotzdem die Schnittstelle gering halten

## Designen Sie zweimal
Der erste versuch etwas zu gestalten oder zu planen, wird niemals der Beste oder der Erfolgreichste sein.
Damit ein gutes Design entstehen kann, muss abgewägt werden, es muss verworfen werden, es muss diskuttiert werden und es muss damit gearbeitet werden. Das ist ja das schöne an Software. Wenn ich merke hey Ansatz XYZ Funktionier nicht oder ich kenne einen einfacheren Weg, dann kann ich das (in der Regel) auch Ändern. Es lohnt sich durchaus sich auch mal die Entwürfe ehrlich miteinander zu vergleichen. Wenn ein alter Entwurf eine spaghetti Implementierung hatte, aber eine geniale Schnittstelle, ist es doch durchaus möglich die Vorteile daraus zu ziehen und daraus zu lernen. Das führt automatisch zu einem besserem Design.

Auch bei Implementierungen gibt es mehrere Möglichkeiten, eine Entscheidung zu treffen? Speicher ich das alles in einem Buffer? Mach ich eine HashMap draus? Ich habe für jeden Weg ja unterschiedliche Optionen offen. Das sollte ich Nutzen und die Vor und Nachteile gegeneinander aufwiegen. Welche Implementierung ist besser in der Performance? Welche ist einfacher? Wichtig ist, dass sowas <b>SCHNELL</b> gehen muss. Ich habe in der Regel
nicht die Zeit Stundenlang über ein Design zu philosphieren. Dabei hilft aber vor allem: Erfahrung.

## Über Kommentare
Gute Dokumentation ist wichtig. Keine Ausreden. Gute Dokumentation erhöht die Codequalität und macht es
einfacher mit bestimmten Abstraktionen zu arbeiten. Es gibt im Wesentlichen ein paar bullshit Ausreden, die Entwickler nutzen, um keine Kommentare zu schreiben. Das ganze läuft unter dem Motto: "... and other hilarious jokes you can tell yourself"

### Guter Code dokumentiert sich selbst
Das ist schlichtweg gelogen. Natürlich gibt es code, der eher die Intention des Autor ausdrückt als 
anderer Code. Also wo die Variablen besser benannt sind, aber WARUM ich etwas tue, also
um eine Metaebene Aufzubauen, oder ein bestimmtes Narrativ zu bekommen für den Code geht nur mit Kommentaren.
Es geht darum, bedeutungsvolle Kommentare zu schreiben, die nicht ein Stoppschild beschreiben,
also das Offensichtliche wiederholen. (Retun Node ... ;) ). Sondern es muss beschrieben werden, was die Rückgabewerte bedeuten, welche Designentscheidungen getroffen wurden.

Besonders bei großen Systemen bedeutet es einen immensen Aufwand das Verhalten einer Schnittstelle 
erst durch den Code zu lesen, statt dass es Erklärt oder Dokumentiert ist. 
<b>Wenn ich den Code erst lesen muss, um zu wissen, was er kann gibt es KEINE Abstraktion </b>
Ohne Kommentare bleiben nur Namen, Typen und Rückgabewerte. Nur damit ist es sehr schwer die Intention auszudrücken. Es macht ja auch Sinn die Implementierung in einem Methodenkommentar grob zu beschreiben, da ich dann nur durch die Schnittstelle auch weiß, wie sich das ganze Intern verhält, ohne dabei den Code gelesen zu haben. Das erfordert allerdings, dass Methodenkommentare aktuell gehalten werden müssen und dass bei anderen Designentscheidungen auch die Kommentare gewartet werden müssen. Das gehört hald einfach dazu.

### Ich habe da keine Zeit für
(Siehe taktische vs Strategische Programmierung). Es gibt immer wichtigere Dinge als Dokumentation und wenn der Projektmanager die Wahl hat zwischen Doku und Feature, wird immer Feature gesagt werden. Die Illusion ist, dass wir den Leuten die Wahl lassen. Die halbe Stunde kann ich mir auch eben nehmen, n paar Zeilen zu schreiben, verweise zu schreiben. Vielleicht auch noch nen Klassenkommentar zu machen, der die Schnittstelle beschreibt, und dann auf die Methoden eingehen. Die Zeit MUSS ich mir einfach nehmen.

### Aber die Kommentare veralten ja..
Ja klar tun sie das, wenn du die Implementierung Änderst und dann den Methodenkopf nicht anpasst.
Oder du vergisst die Kommentare vor den Methoden aufrufen oder ein anderer löscht die Stelle der Doku,
die für dein Feature gebraucht wird(was sowieso nicht vorkommen sollte)...
Reviewe deinen Code, Nutze das Versionierungssystem. Passt der Commit zu dem was du geschrieben hast und spiegeln die Kommentare die Intention wieder? 

### Die Vorteile
Kommentare bieten die Möglichkeit der Metadokumentation. Ich kann das niederschreiben,
was ich im Kopf hatte, als ich das geschrieben habe und kann so dem nächsten
Programmierer somit eine Idee geben, wie ich das ganze gedacht habe,
was ich mir vorgestellt habe etc. Jeder hat ja eine andere Struktur, so kann ich
durch meine Kommentare anderen meine Struktur zeigen und somit mein Design OFFENSICHTLICH machen.

>Dokumentation kann kognitive Last reduzieren. 

Das geschieht, indem alle relevanten Informationen zu dem Code den ich grad geschrieben habe explizit erwähnt werden. So bleiben keine Informationen verborgen und so kann auch jeder damit arbeiten.
Ein gutes Design kann kommentare deutlich reduzieren, ja aber niemals ersetzen.
Kommentare sind keine Fehler. 

### Wie sehen denn gute Kommentare aus?
In der Regel bedarf es dazu guter Konventionen. Wenn ich sowas geordnetes wie javadoc have, sollte
ich es nutzen, weil es ein bereits etabliertes system ist.Es gibt mehrere Arten von Kommentaren:
- Schnittstelle (jdoc methoden)
- Datenstrukturen (Wer greift worauf zu?)
- Implementierung(wie funktioniert die Methode intern)
- Modulübergreifend (welches modul hat welche abhngigkeiten)

Die ersten beiden Kategorien sind die wichtigsten. Kommentare sollen den Code 
nicht wiederholen, sondern das beschreiben was nicht offensichtlich ist.
Also nicht return node sondern ich beschreibe eher im methodenkopf das was die methode machen soll,
worauf der anwender achten muss, wie sie sich sonst verhält. Alles andere innerhalb der 
methode kommentiere ich nur, wenn es nicht offensichtlich ist, oder um die intention besser auszudrücken.
Ich mag es auch gerne bei längeren methoden Kommentare zu nutzen, für visuelle gruppierung.

Auch beliebter fehler ist es in einem Methodenkommentar den Methodenkopf zu beschreiben.
In wie fern entscheidet sich X von Y? Was muss ich beim Einsatz beachten?
Vor allem: Was sagt der Wert über den Zustand der Schnittstelle aus.

Und nochmal: Zustände und Datenstrukturen müssen dokumentiert werden.
Im Prinzip habe ich beim Kommentieren 2 möglich Ebenen: makro und micro.
Die Makroebene soll die Schnittstelle und das generelle High-level verhalten beschreiben.
Die Micro ebene geht im Low level bereich auf die Entscheidungen ein.

Beides zu verwenden ist der Schlüssel zum Erfolg. Es sollte bei Schnittstellen an der Klasse eine Schnittstellenbeschreibung geben, was man von dieser Schnittstelle zu erwarten hat auf einer high-level ebene. Schnittstellenkommentare dürfen auf gar keinen Fall die Besonderheit der Implementierung
beschreiben, da das niemanden in der Schnittstelle interessiert.

### Implementierungskommentare
Das Hauptziel der Implementierungskommentare ist es dem Leser zu erklären,
was der code tut und nicht wie er es tut. Der Author verlangt also Section Kommentare, um die Prozedur auf einer Abstrakten Ebene darzustellen. Ebenfalls verlang er für längere Iterationen Schleifenkommentare, damit der Leser weiß, was in der Schleife geschieht.

### Interessanter Ansatz
Schreibe die Designnotes, Designentscheidungen, Problemlösungen und das allgemeine 
Domönenwissen zur Problemlösung in eines oder mehrere Designdokumente und verweise in den Kommentaren 
auf die Designdokumente. So kann jeder Leser das ganze kreuzweise Referenzieren, wenn es dann mal etwas komplexer wird und man wirklich Hintergrundinformationen zu einem Thema braucht.
Dann kann man sowas wie `// @see DesignDocs/architecture.md`in den code einpflegen

## Über die Benennung 
> _2 Dinge sind wirklich schwer. Variablen benennen und Caches._

Wir gehen in der These davon aus, dass gute Namen von Variablen zu Wartbarem Code führen. Durch Bezeichner können Informationen kommuniziert werden, welche für die Wartung des Codes genutzt werden kann. So hat der Author zum Beispiel einen Riesigen Bug gefunden, welcher über ein halbes Jahr hinweg sine Software geplagt hat. Schuld war falsche oder irreführende Benennung. Der Author rät daher, dass man sich nicht mit Namen zufrieden gibt, die "ziemlich gut sind", sondern mit Namen, die genau passen und wasserdicht sind.

Namen sind eine vereinfachte Form der Abstraktion. Wir meinen eine bestimmte Form, einen Rhytmus eine Melodie oder ein Objekt und wir bezeichnen es. Je genauer oder treffender wir etwas bezeichnen, desto wahrscheinlicher ist es, dass unser Leser das gleiche Bild im Kopf hat.

Namen sollten 2 Eigenschaften haben:
- Präzision
- Konsistenz

Folgende Namen sind ab jetzt tabu:
- data
- row
- count
- object
- result
- Dinge
- ...

Das sind alles zu allgemein gehaltene Namen, die absolut nichts bezeichnen und auch
nicht wirklich Aussagekräftig sind. Wenn es nicht um Mathematische Operationen geht, sollten
x und y eigentlich auch hochgradig illegal sein. Genau so wie i und j ohne den Kontext einer Schleife.
Man kann schon alleine mit dem Namen auf den Zustand und mit dem Typ auf die Konsistenz schließen.
Beispiel: `Boolean IsCursorVisible = true;`

### So bekommt man da Konsitenz rein

Wenn es schwer ist, eine Variable treffend zu benennen,  liegt noch nicht 
genügend Klarheit über Design und Konzept zu grunde. Ich kann hier noch 
kein klares Bild zeichnen, da vielleicht Anforderungen fehlen oder oder...

Namen müssen konsistent eingesetzt werden. So kann man selbst in großen Softwaresystemen
immer den Überblick behalten und viele Fragen klären. 
Konsistenz besteht aus 3 Anorderungen:
- Nutze immer den gleichen Namen für den gleichen Zweck
- Verwende den gewählten Namen niemals für etwas anderes
- Stelle sicher, dass alles mit gleichem Namen auch das gleiche Verhalten hat

><b>Tipp:</b> Für wirklich Präzise Benennung kann man bei wirklich sehr ähnlichen Variablen 
>mit einem Präfix / Suffix System arbeiten. also wenn ich z.B sowas habe wie FileBlock
>kann ich als Präfix sowas wie source oder destination verwenden. Draus wird für Filesystem Operationen
> dann der sourceFileBlock.

### Überflüssige Informationen Vermeidenf
In den meisten Programmiersprachen arbeitet man mit einem Typensystem.
Das Typensystem liefert viele Informationen über die Variable.
Grade in Sprachen wie Java, Rust etc. ist es möglich sehr viele Informationen
über das Typensystem auszudrücken, sodass ich Benennungen wie object
oder class oder FileList aus der Benennung streichen kann, da ja bereits Annotationen
durch das Typensystem existieren. so wird aus fileList List<File> documentsToScan.

Auch durch Klassen oder besimmten Kontext ist es möglich Informationen zu reduzieren.
In einer Klasse namens File muss ich kein Attribut haben, was FileBlock heißt.
Ich kann es also einfach Block nennen. 

## Kommentare zuerst schreiben
Menschen denken sowieso in Schritten und in Prozeduren. Das ist schwer zu ändern.
Das ist einfach so. Und das kann man sich im Designprozess zu Nutze machen.
Ich kann zur Struktur beitragen, indem ich erstmal die Sektionskommentare schreibe.
Also grob erstmal reinkloppen, was ich denn überhaupt da verarbeiten will und davon erwarte.
Dann nen Methoden Kommentar schreiben, was die Schnittstelle ist und dann nachdem das 
Grundgerüst steht weiter in die Tiefe der Implementierung gehen.

Somit weißt du automatisch wieder, wo du dich befindest, wenn du mal 2,3 Tage den Code
nicht angesehen hast und andere werden es dir danken. Der Author empfiehlt das Schreiben
der Kommentare direkt in den Desingprozess mit einzugliedern. Das hilft gegen
technische Schuld.

Wenn der Kommentar schlecht zu schreiben ist, oder schwierig zu beschreiben ist,
liegt Unklarheit vor. Wenn der Kommentar zu komplex ist und viel viel zu lang ist,
deutet das auf eine zu komplexe schnittstelle hin.

## Die Wartung aka. bestehenden Code anpassen

Ein wachsendsendes Softwaresystem fußt immer auf den inkrementell getroffenen Entscheidungen,
welche im Laufe des Designprozesses getroffen wurden. Im Laufe der Warung einer Anwendung ist es wichtig,
Strategisch zu denken. Also eine Investitionsmentalität mit sich zu bringen. Man neigt bei großen Codebases ja dazu,
dass man nur "kleine" Änderungen macht, sodass man nur den kürzesten Weg zum beheben des Problems geht.
Das Problem ist, dass das zu "mülligem" Code führen kann. 

>Ich muss gestehen, dass ich das anders sehe. Das ist son Ding, was man nur macht, 
>wenn man zu 100% die Domäne und das Feature kennt. Außerdem gibt es auch Ecken in einer Codebase
>die nicht getestes sind, wie kann ich da etwas Ändern (außer Benennung), wenn keine Tests vorhanden sind?

Der Author empfiehlt auch bei kleinen Änderungen auf die Abstratkionsebene einzugehen und die Codebase aus
der Makroebene heraus zu sehen (oder zumindest das Feature). Das finde ich löblich, aber ist im "alltag" kaum umzusetzen,
wenn die Vorraussetzungen nicht stimmen. Was aber möglich ist: Die Schnittstelle zu verbessern durch Kommentare, Schnittstellenkommentare für die Klassen, Methodenkommentare und Implementierungskommentare. Wenn ich wirklich die 
Funktionsfähigkeit einer Funktion beweisen kann (weil ich sie grade Teste) kann ich ja auchmal 1,2 If verschachtelungen auflösen.

>Ich persönlich finde den "Pfadfinder" Gedanken von Uncle Bon ganz gut - aber alles Aufräumen zu wollen, 
> für naiv und unrealistisch (grade wenn es legacycode ist) Wer weiß vielleicht änder sich diese Einstellung 
>ja noch bei den kommenden Büchern.

<b>Verbessern Sie das Design nicht, machen Sie es vermutlich noch schlimmer </b

### Kommentare pflegen

>Merke: Kommentare kann man besser anpassen, wenn sie nahe am Code sind.

Die Pflege von Kommentaren sollte vor allem der Kommentare gelten, die durch Konventionen vereinbart wurden.
z.B Phpdoc, javadoc oder doxygen. Allgemein sollte gelten: Je weiter ein kommentar vom Code enfternt ist,
desto abstrakter sollte er sein. Dokumentation sollte also da platziert werden, wo Sie gelesen wird. Also im Code und
nicht im Commitlog. Wenn ein Schweres Problem aufgetreten ist, sollte die Lösung oder die Begründung warum was eingefügt wurde 
in den Code geschrieben werden, statt das ganze im commitlog "verrotten" zu lassen.

Es gilt ebenfall Duplikate zu vermeiden. Gerade Variablen die nach außer geöffnet sind oder Configs sind anfällig für sowas.
Dokumentier die Sachen an einer Zentralen Stelle. So musst du nicht überall die Implementierung dokumentieren.
Wenn es keinen wirklichen Zentralen Ort gibt, sollten hier die Designnotes herhalten. (Die übergeordnete Entwicklerdokumentation)
In den meisten Fällen reicht ja ein Verweis auf die Designdokumentation. Aber: Dann musst du die Designdocs aktualisieren.

Wenn ich mit Bibliotheken oder mit 3rd Party dependencys oder Services arbeite, reicht es in der Regel das WARUM
an die Externe Dokumentation auszulagern. Also ein `//@see ...`.
Ebenfalls zum pflegen der Kommentare sollten regelmäßig die Diffs angesehen werden.
Es ist schlau das wie bei IKOffice vor einem Commit zu machen. Dort schauen wir jeden Commit nochmal komplett durch.

Im Allgemeinen ist es schwerer Code zu pflegen, der nahe an der Implenterung ist. Wenn sich die Implementierung änder, muss sich auch der Methodenkommentar ändern, wenn ich allerdings z.B nur den methodenkörper ändere, muss ich nicht z.B den Schnittstellenkommentar anrühren.
Das muss ich erst bei nem Refactoring. 

## Konsistenz

Konsistenz ist DAS Mittel der Wahl, um gegen Komplexität anzugehen. Ist ein System konsistent ist es nicht nur verlässlich, 
sondern auch integer und verringert den Schulungsbedarf. Ein gutes Beispiel für Konsistenz befindet sich bei meinem Arbeitgeber
IKOffice. Jede Entity hat eine Form, welche das Gui beinhaltet, eine Impl die das Verhalten beinhaltet, oftmals eine Managerklasse, die als Übergeordneter Controller dienen kann, eine Editorklasse, die ein Interface für die einfache berarbeitung bietet und für den Kunden eine Ableitung mit dem Selben Namen der Klasse aus dem Kern der Anwendung nur mit dem Kunden davor also `KundePurchaseOrderEditor`
Das ist ein gutes Beispiel für KOnsistenz in der Benennung. 

Konsistenz im Coding Stil ist auch eine gute Form. Es gibt ja die Tolle Regel "When you're in rome, do as the romans do". 
Das macht es leicht eine Einheitliche Linie zu fahren, was den Code angeht und damit fügt sich der Code auch nahtlos in dern restlichen code ein.
Schnittstellen und implementierung der Interfaces sind auch ein gutes Beispiel für Konsistenz. Wenn ich bereits einmal eine Schnittstelle und ihre 
Implementierung verstanden habe, ist es ein leichtes einene weitere Implementierung anzusetzen (insofern die Implementierung dokumentiert ist), weil ich dann weiß, was ich zu erwarten habe. 

Design Patterns sind z.B auch ein gutes Beispiel für Konsistenz, da sie (wenn sie nicht total obskur sind) die Anwendung wartbarer machen.
Konsistenz kan über die Zeit durch unachtsamkeit gefährdet werden. (Neulinge sind da sehr anfällig für - ja auch ich).
Man kann die Konsistenz sicherstellen, indem z.B Coding oder Architekturrichtlinien festgehalten werden. 

Am besten kann man z.B Coding Conventions einhalten, indem man ein Tool zur Prüfung des Codes abrichtet.
Grad Line endings können da gerne mal zu einem Problem werden, wenn man auf unterschiedlichen Plattformen entwickelt.
Ebenfalls führen Code Reviews zu mehr Konsistenz, da der reviewer die Konventionen durchsetzen kann.

Bestehende Konventionen zu ändern zeugt auch nicht von Konsistenz. Auch wenn es die "bessere Idee" ist, lass es.
Erst wenn 20 Leute in einer Organisation alle dafür stimmen Regel X über Board zu werfen einfach weil es keinen Sinn macht, sure go ahead
aber wenn es um Konsistenz geht behält man die Regeln bei, auch um der Regel willen. (So spart man sich auch Entwicklungszeit,
weil man so Immun gegen jedes neue Framework wird)

## Guter Code ist offensichtlich

Unklarheit soft für Komplexität und tritt auf, wenn Informationen fehlen und nicht transportiert werden.
Die Lösung wäre es den Code so zu schreiben, dass er explizit die Anforderungen kommuniziert.
Wenn Code offensichtlich ist, (langweilig) kann der Code schnell gelesen werden und
das zusammentragen von infos geht schneller, weil man jetzt den Code nicht mehr verstehen oder interpretieren muss.
Der Leser bestimmt, wie offensichtlich Code ist. Offensichtlichkeit stellt man durch code Reviews fest.
Ich habe auch gute Erfahrungen damit gemacht, auch den code mal auf einem anderen Gerät zu lesen, z.B auf Github.

### Was macht Code offensichtlich?
Gute, aussagekräftige Namen und Kosistenz. Leerräume Nutzen, um code zu strukturieren. Also immer Codeblöcke die den gleichen gedanken hatten, gruppieren. Auch dokumentation also methodenköpfe gerne einrücken und zwischenzeilen setzen, wenns zuviel wird.
Auch in Schleifenköpfen mehr Whitespace verwenden und Kommentare Setzen.

### Was macht Code __NICHT__ offensichtlich?
Wenn Bedeutung und Verhalten von Code nicht durch schnelles durchfliegen verstanden werden können, ist das ein absolutes alarmzeichen.
Eventgetriebene Programmierung macht viele Sachen schwerer, da die Events meist von den unterschiedlichen Modulen gerufen werden, oder hald von außen,
was das Nachvollziehen des call Stacks schwerer macht. Tuples in statischen Sprachen sind auch schwierig. Also Record und Pair, weil dann jeder Wert 
und deren Bedeutung Dokumentiert werden muss. Auch die Methoden(getKey, getValue) verschleiern das ganze. **Allgemein sollte sich software leicht lesen
lassen und nicht leicht schreiben lassen.** Unterschiedliche Typen verwenden für den gleichen Zweck ist auch eine schlechte Idee.
Code der die Erwartung verletzt ist auch richtig mies. Also grad so Atombomben Code, der dir auf die Füße fällt ist richtig mies.
Also wenn der Code etwas macht und der Leser erwartet X es aber nicht im Code kommuniziert wird.

## Softwaretrends

### OOP
Objektorientierung ist das dominierende Paradigma der letzen Jahre. Viele der Konzepte können genutzt werden,
um bessere Softwaredesigns zu schaffen. z.B Information Hiding ist ausgesprochen praktisch. Ousterhout spricht 2 mögliche Auspräungen in der
Objektorientierung an. Da wäre einmal die Schnittstellenvererbung. Darunter versteht der abstrakte Methoden, welche die Kindklassen dazu zwingen die Signatur zu implementieren. Und dann die Implementierungsvererbung. Damit meint er die "klassische" vererbung. Diese Art der Vererbung __kann__ den Code Reduzieren. Das große Problem an der Implementierungsvererbung ist, dass die Vererbung an sich Abhängigkeiten zwischen eine Kind und Ihrer Elternklasse erzeugt. Es werden Attribute mitgenutzt und damit geht der Gedanke einer "sauberen" Schnittstelle flöten. Der Author zieht auch hier Komposition klar vor. Der Author schlussfolgert: OOP alleine verwenden, macht kein gutes Softwaredesign. Es ist ein Tool.

### Agile Entwicklung
Der Grundgedanke der agilen Entwicklung ist, dass die Entwicklung eine inkrementelle und iterative Strategie verfolgen soll. 
Der Vorteil der agilen Entwicklung besteht in der inkrementellen Verbesserung des Produkts. Der Author sieht allerdings 
ein Risiko in der agilen Entwicklung, wenn man ausschließlich Features bearbeitet, denn dies führt zu taktischer statt strategischer Programmierung.
Seiner Meingung nach sollte das Ziel solcher Entwicklungsschritte immer die Abstraktion sein.

### Unit tests
Unittests sind Codeabschnitte, die lösgelöst vom Gesamtsystem getestet werden. Unittests sind von Vorteil, 
da Sie das Refaktorieren erleichtern. Außerdem werden so viel eher Fehler aufgedeckt, bevor sie die Produktion erreichen.
Der Author hält prinzipiell Unit und Systemtests (Integrationstests für wichtig und wertvoll).

### TDD
Hierbei geht es datum zuerst die Tests zu schreiben und dann die Implementierung geschehen zu lassen. 
Der Author sieht dabei die gefahr, dass das gesamtdesign vernachlässigt wird,
da nur von einer Implementierung (und Refaktorierung) zur nächsten gesprungen wird 
und nicht das Design als ganzes in Frage gestellt wird.

### Design Patterns
Designpatterns lösen bestimmte vorhandene Probleme in der Softare durch ein vorgefertigtes Design.
Es ist prinzipiell nicht verkehrt etwas wiederzuverwenden. Obacht: Jedes verwendete Pattern kann 
die Komplexität der Anwendung erhöhen. 

### Getter und Setter
Laut Ousterhout sorgt das für eine viel zu flache Schnittstelle der Klasse - Er sieht es also als ein Anti Pattern.

## Performance
>Wie sehr sollte ich mich während des normalen Entwicklungsprozesses um performance kümmern?

2 mögliche Wege hier: Alles mitnehmen, was geht und damit für Überkomplexen Code sorgen (SMF Forum) oder
garnicht drauf eingehen und vollkommen ignorieren, bis es zu spät ist(Bestimmte proprietäre Software).
Das beste wäre ein Zwischenweg. Regelmäßiges Benchmarken der Funktionen ist also ein muss. Dadurch wird sichtbar,
welche Operationen eher "teuer" und eher "günstig" sind im Sinne der Performance. 












