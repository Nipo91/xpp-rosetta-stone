# Was der Code aufruft

> **Pad-Block „Was der Code aufruft“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 2 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *obj.methode() = du rufst den Standard; rechts steht, was zurückkommt*

### `addRange(fieldNum(T, F)).value(…)`

**Auf dem Pad:** Filter auf eine Spalte setzen

Ein Filter auf eine Spalte der Query. value() nimmt Text – deshalb queryValue(x), das Sonderzeichen maskiert. Mehrere addRange auf dasselbe Feld sind ein ODER.

### `addDataSource(tableNum(T))`

**Auf dem Pad:** Tabelle an die Query hängen

Hängt eine Tabelle an eine Query oder, als Kind einer anderen Data Source, als Join.

### `addLookupfield(fieldNum(T, F))`

**Auf dem Pad:** Spalte im eigenen Lookup zeigen (SysTableLookup)

Im eigenen Lookup (SysTableLookup): Diese Spalte wird in der Auswahlliste gezeigt; true markiert das Feld, dessen Wert zurückkommt.

### `queryRun.next() / .get(tableNum(T))`

**Auf dem Pad:** Query ausführen, Datensätze durchlaufen, Puffer holen

Durchlaufen einer Query: next() holt den nächsten Treffer, get(tableNum(T)) liefert den Puffer der Tabelle T aus diesem Treffer.

### `selectForUpdate(true) → insert() / update()`

**Auf dem Pad:** Puffer zum Ändern sperren, dann schreiben

Markiert den Puffer als „zum Ändern gesperrt“; danach sind insert() und update() erlaubt. Nur innerhalb von ttsBegin/ttsCommit.

### `addEnd(…) / add(…)`

**Auf dem Pad:** Liste bzw. Set oder Map füllen

List füllt man mit addEnd (oder addStart), Set und Map mit add bzw. insert. Alle drei sind typisiert (Types::String, Types::Record).

### `getEnumerator() / moveNext() / current()`

**Auf dem Pad:** Liste durchlaufen

Das Durchlaufen von List, Set und Map: getEnumerator() liefert den Zeiger, moveNext() schaltet weiter und liefert false am Ende, current() ist das aktuelle Element.

```xpp
ListEnumerator en = list.getEnumerator();
while (en.moveNext())
{
    info(en.current());
}
```

### `visible(false) / enabled(false)`

**Auf dem Pad:** Control verstecken / sperren

Controls zur Laufzeit schalten: visible blendet aus, enabled sperrt. Das Control holt man über seinen Namen im Form-Code (AutoDeclaration) oder über element.design().

### `strFmt("%1 …", x)`

**Auf dem Pad:** Text mit Platzhaltern zusammensetzen

Baut Text mit Platzhaltern %1, %2 …; auch für Labels mit Platzhaltern. Zahlen und Datum werden passend formatiert.

### `info() / warning() / error(), checkFailed()`

**Auf dem Pad:** Meldung ins Infolog; Prüfung meldet und gibt false

info, warning und error schreiben ins Infolog. checkFailed("…") schreibt eine Warnung und liefert false – das Muster für Prüfmethoden: return checkFailed(…).

## Verknüpft

- [Alle Blöcke](../README.md)
