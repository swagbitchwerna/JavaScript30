Bubble Sort ist einer der einfachsten Sortieralgorithmen. Er funktioniert, indem er immer zwei benachbarte Elemente miteinander vergleicht und sie vertauscht, wenn sie in der falschen Reihenfolge stehen.

Der Name „Bubble Sort“ kommt daher, dass die größeren Werte bei aufsteigender Sortierung Schritt für Schritt nach oben bzw. ans Ende des Arrays „blubbern“.

Wir gehen deinen Code Zeile für Zeile durch.

## 1. Das Ausgangsarray

javascript

```javascript
let arr = [25, 12, 22, 11];
```

Wir haben vier Zahlen, die aufsteigend sortiert werden sollen:

text

```text
[25, 12, 22, 11]
```

Das gewünschte Ergebnis:

text

```text
[11, 12, 22, 25]
```

## 2. Die äußere Schleife

javascript

```javascript
for (let i = 0; i < arr.length - 1; i++) {
```

- `let i = 0`: Wir starten bei 0.
- `i < arr.length - 1`: Die Schleife läuft, solange `i` kleiner als 3 ist.
- `i++`: Nach jedem Durchlauf wird `i` um 1 erhöht.

Aber warum brauchen wir diese Schleife überhaupt?

Weil ein einziger Durchlauf durch das Array nicht unbedingt ausreicht, um alle Zahlen richtig zu sortieren.

Die äußere Schleife sorgt dafür, dass wir mehrere Durchgänge machen.

Bei unserem Array mit vier Elementen brauchen wir maximal drei Durchgänge.

## 3. Die innere Schleife

javascript

```javascript
for (let j = 0; j < arr.length - i - 1; j++) {
```

Das ist die eigentliche Arbeits-Schleife von Bubble Sort.

Sie kümmert sich darum, die benachbarten Elemente miteinander zu vergleichen.

- `j = 0`: Wir beginnen beim ersten Element.
- `j < arr.length - i - 1`: Wir laufen durch das Array.
- `j++`: Wir gehen jeweils eine Position weiter.

Warum ziehen wir `i` und `1` ab?

Das ist einer der wichtigsten Punkte bei Bubble Sort:

Nach jedem vollständigen Durchlauf steht die größte noch nicht sortierte Zahl bereits an ihrer endgültigen Position ganz rechts.

Wir müssen diese Position bei den nächsten Durchläufen nicht mehr berücksichtigen.

Deshalb wird der zu durchlaufende Bereich mit jedem Durchgang kleiner.

## 4. Der Vergleich

javascript

```javascript
if (arr[j] > arr[j + 1]) {
```

Hier passiert die eigentliche Sortierentscheidung.

Wir vergleichen immer zwei benachbarte Elemente:

- `arr[j]`: Das aktuelle Element.
- `arr[j + 1]`: Das direkt dahinterliegende Element.

Wenn das linke Element größer ist als das rechte, stehen sie in der falschen Reihenfolge.

Dann müssen wir sie vertauschen.

Beispiel:

text

```text
[25, 12, 22, 11]
```

Wir vergleichen:

text

```text
25 > 12 ?
```

Ja\!

Also müssen die beiden Zahlen ihre Position wechseln.

## 5. Das Vertauschen (Swap)

javascript

```javascript
let temp = arr[j];
arr[j] = arr[j + 1];
arr[j + 1] = temp;
```

Hier verwenden wir eine Hilfsvariable (`temp`), um zwei Werte zu vertauschen.

Warum brauchen wir diese?

Stell dir vor, wir würden einfach Folgendes machen:

javascript

```javascript
arr[j] = arr[j + 1];
arr[j + 1] = arr[j];
```

Das würde nicht funktionieren\!

Denn sobald wir die erste Zeile ausführen, überschreiben wir den ursprünglichen Wert von `arr[j]`.

Deshalb speichern wir ihn vorher zwischen.

So funktioniert der Swap:

## Beispiel: 25 und 12 tauschen

SCHRITT 1 – URSPRÜNGLICH

# 25

arr\[j\]

# 12

arr\[j+1\]

SCHRITT 2 – ZWISCHENSPEICHER

javascript

```javascript
let temp = 25;
```

Die 25 wird gesichert.

SCHRITT 3 – 12 NACH LINKS

javascript

```javascript
arr[j] = 12;
```

SCHRITT 4 – 25 NACH RECHTS

javascript

```javascript
arr[j + 1] = temp;
```

Ergebnis# 12

# 25

## 6. Der komplette Ablauf anhand unseres Arrays

Jetzt schauen wir uns an, was tatsächlich passiert.

Ausgangslage:

text

```text
[25, 12, 22, 11]
```

Durchgang 1 (`i = 0`)

| Vergleich | Aktion | Array danach |
| --- | --- | --- |
| 25 und 12 | Tauschen | \[12, 25, 22, 11\] |
| 25 und 22 | Tauschen | \[12, 22, 25, 11\] |
| 25 und 11 | Tauschen | \[12, 22, 11, 25\] |

25 steht jetzt richtig\!Die größte Zahl ist ganz rechts angekommen.

Durchgang 2 (`i = 1`)

| Vergleich | Aktion | Array danach |
| --- | --- | --- |
| 12 und 22 | Nichts | \[12, 22, 11, 25\] |
| 22 und 11 | Tauschen | \[12, 11, 22, 25\] |

22 steht jetzt richtig\!Durchgang 3 (`i = 2`)

| Vergleich | Aktion | Array danach |
| --- | --- | --- |
| 12 und 11 | Tauschen | \[11, 12, 22, 25\] |

Fertig sortiert\!## 7. Warum funktioniert Bubble Sort überhaupt?

Das ist eigentlich die interessanteste Frage.

Der Algorithmus funktioniert aufgrund eines einfachen Prinzips:

Nach jedem vollständigen Durchgang steht das größte Element des noch unsortierten Bereichs garantiert an seiner endgültigen Position.

Warum?

- Wir vergleichen immer zwei benachbarte Elemente.
- Ist das linke größer, tauschen wir sie.
- Dadurch wandert die jeweils größere Zahl immer eine Position nach rechts.
- Das wiederholen wir bis zum Ende des noch unsortierten Bereichs.
- Somit muss die größte Zahl dieses Bereichs am Ende angekommen sein.

Das bedeutet: Wir müssen sie danach nie wieder anfassen.

Nach jedem Durchgang ist also ein weiteres Element rechts endgültig sortiert.

## 8. Warum wird die innere Schleife immer kürzer?

Schau dir diese Zeile noch einmal an:

javascript

```javascript
j < arr.length - i - 1
```

| Durchgang | i | Vergleichsanzahl |
| --- | --- | --- |
| 1 | 0 | 3 |
| 2 | 1 | 2 |
| 3 | 2 | 1 |

Das `- i` sorgt dafür, dass die bereits sortierten Elemente am rechten Rand übersprungen werden.

Das letzte `- 1` ist notwendig, weil wir immer `arr[j]` mit `arr[j + 1]` vergleichen. Wir dürfen also nicht über den letzten gültigen Index hinausgehen.

## 9. Die wichtigsten Erkenntnisse

- Die äußere Schleife bestimmt, wie oft wir das Array durchlaufen.
- Die innere Schleife vergleicht benachbarte Elemente.
- `if` entscheidet, ob ein Tausch notwendig ist.
- `temp` ermöglicht das sichere Vertauschen zweier Werte.
- Nach jedem Durchgang steht eine weitere Zahl rechts an ihrer endgültigen Position.
- Deshalb wird die innere Schleife immer kürzer.

Noch eine interessante Information: Bubble Sort hat im schlechtesten und durchschnittlichen Fall eine Zeitkomplexität von $O(n^2)$. Das bedeutet, dass die Anzahl der Vergleiche bei großen Arrays sehr schnell steigt.

## 10. Kleine Verständnisübung

Ich würde dir gerne eine Frage stellen, um zu überprüfen, ob du das Prinzip wirklich verstanden hast.

Warum wird die innere Schleife bei jedem Durchgang um eine Position kürzer?

a Weil die größte Zahl nach jedem Durchgang bereits an ihrer endgültigen Position steht.

Weil JavaScript nach jedem Durchgang weniger Array-Elemente speichert.

Weil die innere Schleife sonst unendlich laufen würde.

 Antwort überprüfen
