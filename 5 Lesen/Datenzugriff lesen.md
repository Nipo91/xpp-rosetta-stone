# Datenzugriff lesen

> **Pad-Block „Datenzugriff lesen“, Familie Lesen**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 2 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Feldnamen groß (AccountNum), Puffer klein (custTable), _param = Methodenparameter.*

### `select firstOnly t where t.Id == _id;`

**Auf dem Pad:** Einen Datensatz holen

Holt genau einen Datensatz in den Puffer t. Ohne firstOnly würde der erste Treffer landen, die Datenbank aber alle liefern.

### `select forUpdate t where ...`

**Auf dem Pad:** Zum Ändern sperren, nur in ttsBegin / ttsCommit

Sperrt den Satz zum Ändern – Pflicht vor update() und delete(), und nur innerhalb von ttsBegin/ttsCommit.

### `while select t where ... { }`

**Auf dem Pad:** Schleife über alle Treffer

Die Schleife über alle Treffer; t ist in jedem Durchlauf der aktuelle Satz.

```xpp
while select order where order.Status == MyStatus::Open
{
    info(order.OrderId);
}
```

### `join b where b.Id == a.Id`

**Auf dem Pad:** Nur mit Gegenstück

Inner Join: nur Sätze, die ein Gegenstück haben. Beide Puffer sind danach gefüllt.

### `outer join`

**Auf dem Pad:** Auch ohne Gegenstück

Auch Sätze ohne Gegenstück; der Puffer der zweiten Tabelle bleibt dann leer.

### `exists join / notExists join`

**Auf dem Pad:** Nur prüfen, ob Gegenstück da

Nur prüfen, ob es ein Gegenstück gibt (oder keins) – die Felder der zweiten Tabelle werden nicht geholt, das ist schneller.

### `ttsBegin; ... ttsCommit;`

**Auf dem Pad:** Transaktion: alles oder nichts

Transaktion: Alles dazwischen wird ganz oder gar nicht geschrieben. Verschachtelte ttsBegin zählen hoch, erst das letzte ttsCommit schreibt.

### `insert_recordset / update_recordset / delete_from`

**Auf dem Pad:** Mengenweise, eine SQL-Anweisung

Mengenoperationen in einer SQL-Anweisung statt Satz für Satz – deutlich schneller, aber die Tabellenmethoden insert/update/delete laufen nicht (außer die Tabelle erzwingt es).

### `t.insert() / .update() / .delete()`

**Auf dem Pad:** Einzelsatz, ruft Tabellenmethoden

Einzelsatz: ruft die Tabellenmethoden samt eigener Logik. doInsert, doUpdate, doDelete umgehen sie.

## Verknüpft

- [Alle Blöcke](../README.md)
