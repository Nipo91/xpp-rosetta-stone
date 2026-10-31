# Query bauen

> **Pad-Block „Query bauen“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 3 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *q = Query, qbds = Datenquelle darin, qr = der Lauf · T Tabelle, F Feld*

### `Query q = new Query();`

**Auf dem Pad:** leere Query; oder new Query(queryStr(MyQuery))

Eine leere Query, der man Data Sources anhängt. Alternativ new Query(queryStr(MyQuery)) für eine im AOT definierte Query.

### `QueryBuildDataSource qbds = q.addDataSource(tableNum(T));`

**Auf dem Pad:** Tabelle anhängen

Die erste Tabelle. qbds ist der Griff für Ranges, Sortierung und Joins.

### `qbds.addRange(fieldNum(T, F)).value(queryValue(x));`

**Auf dem Pad:** Filter; queryValue maskiert Sonderzeichen

Filter auf ein Feld; queryValue maskiert Sonderzeichen wie * oder , im Wert.

### `qbds.addRange(…).value(SysQuery::range(a, b));`

**Auf dem Pad:** von-bis; SysQuery::valueNot(x) für „nicht“

SysQuery baut Range-Texte: range(a, b) für von-bis, valueNot(x) für ungleich, valueUnlimited() für „alles“, valueEmptyString() für leer.

### `qbds.addSortField(fieldNum(T, F), SortOrder::Descending);`

**Auf dem Pad:** Sortierung

Sortierung nach einem Feld; mehrere addSortField ergeben die Reihenfolge.

### `QueryBuildDataSource c = qbds.addDataSource(tableNum(U));`

**Auf dem Pad:** Kind-Tabelle: Join

Eine Kind-Data-Source unter der ersten – das ist der Join.

### `c.addLink(fieldNum(T, Id), fieldNum(U, Id)); c.joinMode(JoinMode::ExistsJoin);`

**Auf dem Pad:** Verknüpfung + Join-Art (Inner, Outer, Exists, NoExists)

addLink verknüpft die Felder, joinMode sagt die Art: InnerJoin (nur mit Gegenstück), OuterJoin (auch ohne), ExistsJoin (nur prüfen, Felder der Kind-Tabelle nicht holen), NoExistsJoin.

### `qbds.clearRanges(); qbds.clearDynalinks();`

**Auf dem Pad:** Filter löschen / dynamische Verknüpfung zur Eltern-Form lösen

clearRanges löscht alle Filter; clearDynalinks löst die dynamische Verknüpfung zur übergeordneten Form (Master/Detail), damit eine Form eigenständig filtert.

### `qr.changed(tableNum(T))`

**Auf dem Pad:** hat sich der Satz dieser Tabelle seit next() geändert (bei Joins)

Bei Joins: liefert true, wenn sich der Satz dieser Tabelle seit dem letzten next() geändert hat – so erkennt man den Kopfwechsel in einer Kopf-Zeilen-Schleife.

### `qr.prompt();`

**Auf dem Pad:** Query-Dialog zeigen (Benutzer filtert)

Zeigt dem Benutzer den Query-Dialog zum Filtern, bevor die Query läuft.

### `QueryRun qr = new QueryRun(q);`

**Auf dem Pad:** ausführbares Objekt zur Query

Macht aus der Query ein ausführbares Objekt.

### `while (qr.next()) { … }`

**Auf dem Pad:** next() schaltet zum nächsten Treffer, false am Ende

Die Schleife: next() schaltet zum nächsten Treffer und liefert false, wenn keiner mehr kommt.

```xpp
Query q = new Query();
QueryBuildDataSource qbds = q.addDataSource(tableNum(SalesTable));
qbds.addRange(fieldNum(SalesTable, Status)).value(queryValue(MyStatus::Open));
QueryRun qr = new QueryRun(q);
while (qr.next())
{
    SalesTable order = qr.get(tableNum(SalesTable));
    info(order.OrderId);
}
```

### `t = qr.get(tableNum(T));`

**Auf dem Pad:** Puffer der Tabelle aus dem aktuellen Treffer

Holt den Puffer der Tabelle T aus dem aktuellen Treffer. Bei Joins je Tabelle ein get.

## Verknüpft

- [Alle Blöcke](../README.md)
