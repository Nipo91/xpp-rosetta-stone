# Datentypen

> **Pad-Block „Datentypen“, Familie Lesen**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 3 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Leer ist: 0, "", 1\1\1900, false, NoYes::No – Prüfung mit if (!x).*

### `int / int64`

**Auf dem Pad:** Ganze Zahl; RecId ist int64, 0 = kein Datensatz

Ganze Zahlen; int64 für große Werte und für RecId. Eine RecId von 0 heißt: kein Datensatz – if (t.RecId) ist die übliche Prüfung.

### `real`

**Auf dem Pad:** Dezimalzahl; / liefert real, div und mod bleiben int

Dezimalzahl. Division mit / liefert real; div und mod sind ganzzahlige Division und Rest.

### `str / str 10`

**Auf dem Pad:** Text, leer = ""; Länge optional. Verketten mit +, strFmt

Text; str 10 begrenzt auf zehn Zeichen. Leerer Text ist "", es gibt kein null. Verketten mit +, Formatieren mit strFmt.

### `boolean`

**Auf dem Pad:** true / false; jeder Wert ist als Bedingung nutzbar (0, "", leer = false)

true oder false. In X++ zählt jeder Wert als Bedingung: 0, "" und ein leerer Puffer sind false, alles andere true – darum liest man oft if (custTable) statt if (custTable.RecId != 0).

```xpp
if (!order)                 // leerer Puffer = false
    throw error("Kein Auftrag.");
```

### `date / utcDateTime`

**Auf dem Pad:** Datum 22\06\2026 / Datum + Zeit in UTC; rechnen nur mit DateTimeUtil

date ist ein Datum ohne Zeit (Literal 21\11\2026), utcDateTime Datum und Zeit in UTC. Rechnen mit DateTimeUtil (addDays, date, newDateTime).

### `enum`

**Auf dem Pad:** Aufzählung NoYes::Yes; intern 0, 1, 2 – enum2Str gibt das Label

Aufzählung mit festen Werten, geschrieben Enum::Wert. Intern eine Zahl; enum2Str liefert das Label für die Anzeige.

### `container`

**Auf dem Pad:** Werteliste [42, "Kenny", true]; conPeek(c, 1), conLen(c), c += [x]

Eine Werteliste beliebiger Typen: c = [1, "a", true]. Lesen mit conPeek(c, 1) (1-basiert!), Länge conLen, anhängen c += [x].

### `EDT (CustAccount)`

**Auf dem Pad:** Erweiterter Typ: Basistyp plus Länge, Label, Beziehung

Extended Data Type: ein Basistyp (str, int, date …) mit Länge, Label und Beziehung, unter eigenem Namen. Jedes Tabellenfeld trägt einen EDT – daher weiß die Form, wie breit ein Feld ist und wohin ein Lookup springt. Im Code benutzt man den EDT-Namen wie einen Typ.

```xpp
CustAccount custAccount;    // EDT, dahinter str 20 mit Beziehung zu CustTable
custAccount = order.CustAccount;
```

### `CustTable custTable;`

**Auf dem Pad:** Tabellenpuffer = ein Datensatz; leer bei RecId 0

Ein Tabellenpuffer ist ein Datensatz: nach select gefüllt, davor leer (RecId 0). Felder mit Punkt: custTable.AccountNum.

### `int2Str(i) / num2Str(r, 1, 2, 1, 0) / enum2Str(e) / str2Int(s) / any2Str(x)`

**Auf dem Pad:** Umwandlungen in und aus Text

Umwandlungen: int2Str, num2Str(real, Länge, Dezimalen, Dezimaltrenner, Tausendertrenner), enum2Str, str2Int, any2Str für alles. Datum: date2Str, str2Date.

## Verknüpft

- [Alle Blöcke](../README.md)
