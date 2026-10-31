# Data Source im Code (T_ds)

> **Pad-Block „Data Source im Code (T_ds)“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 2 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Im Form-Code: T = aktueller Datensatz (Puffer), T_ds = die Data Source.*

### `T_ds.research(true);`

**Auf dem Pad:** Query neu ausführen, Position halten

Führt die Query der Data Source neu aus. true hält die Position im Grid; ohne Argument springt der Cursor an den Anfang.

### `T_ds.refresh(); / T_ds.reread();`

**Auf dem Pad:** Anzeige erneuern / Satz aus der DB neu lesen

refresh zeichnet die Anzeige des Puffers neu (nach einer Änderung im Puffer); reread liest den aktuellen Satz aus der Datenbank nach (nach einem update() von außen).

### `T_ds.executeQuery();`

**Auf dem Pad:** Query neu ausführen (nach Range-Änderung)

Wie research, aber ohne die Position zu halten – typisch nach einer geänderten Range.

### `T_ds.query().dataSourceTable(tableNum(T)).addRange(…)`

**Auf dem Pad:** Range zur Laufzeit setzen

Zur Laufzeit eine Range auf die Query der Data Source setzen; danach executeQuery oder research.

```xpp
SalesTable_ds.query().dataSourceTable(tableNum(SalesTable))
    .addRange(fieldNum(SalesTable, CustAccount)).value(queryValue(custAccount));
SalesTable_ds.executeQuery();
```

### `for (t = T_ds.getFirst(1); t; t = T_ds.getNext()) { }`

**Auf dem Pad:** markierte Datensätze durchlaufen (Grid-Auswahl)

Die im Grid markierten Sätze durchlaufen: getFirst(1) liefert den ersten markierten, getNext den nächsten, leer am Ende.

```xpp
SalesTable order;
for (order = SalesTable_ds.getFirst(1); order; order = SalesTable_ds.getNext())
{
    MyBillingLogic::construct().processOrder(order);
}
```

### `T_ds.positionToRecord(t); T_ds.findRecord(t);`

**Auf dem Pad:** Cursor auf einen Satz stellen

Setzt den Cursor auf einen bestimmten Satz; findRecord sucht ihn in der aktuellen Query und positioniert.

### `T_ds.allowEdit(false); allowCreate(false); allowDelete(false);`

**Auf dem Pad:** Rechte je Data Source

Rechte für die ganze Data Source zur Laufzeit: bearbeiten, anlegen, löschen. Für ein einzelnes Feld: T_ds.object(fieldNum(T, F)).allowEdit(false).

### `T_ds.object(fieldNum(T, F)).visible(false);`

**Auf dem Pad:** Feld der Data Source: visible, allowEdit, mandatory

Das Data-Source-Feld (FormDataObject): visible, allowEdit, mandatory – gilt für alle Controls, die an dieses Feld gebunden sind.

### `T_ds.create(); T_ds.write(); T_ds.delete();`

**Auf dem Pad:** Satz anlegen / speichern / löschen wie der Benutzer

Dasselbe wie der Benutzer: neuen Satz anlegen, speichern, löschen – inklusive validateWrite und der Form-Methoden.

### `T_ds.active()`

**Auf dem Pad:** ist das der aktive Satz; T selbst = Puffer des aktuellen Satzes

Ob die Data Source gerade einen aktiven Satz hat; der Puffer selbst ist einfach T (der Tabellenname) im Form-Code.

## Verknüpft

- [Alle Blöcke](../README.md)
