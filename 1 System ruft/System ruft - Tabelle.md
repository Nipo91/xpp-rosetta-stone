# System ruft: Tabelle

> **Pad-Block „System ruft: Tabelle“, Familie System ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 4 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Aus Klasse und Batch läuft kein validate… automatisch – selbst aufrufen. doInsert / doUpdate / doDelete umgehen alles.*

### `initValue()`

**Wann:** Neuer Datensatz (Form oder Code)  
**Auf dem Pad:** Nach super(): Standardwerte setzen – Datum, Firma, Parameterwerte; nichts, was vom Kontext der Form abhängt

Beim Anlegen eines neuen Satzes, egal ob aus der Form oder aus Code. super() setzt die Standardwerte der EDTs; danach eigene Vorbelegungen aus Parametern, Datum oder Firma. Nichts, was vom Kontext einer bestimmten Form abhängt.

```xpp
public void initValue()
{
    super();
    this.TransDate = DateTimeUtil::date(DateTimeUtil::utcNow());
    this.Currency  = MyParameters::find().DefaultCurrency;
}
```

### `validateField(_fieldId)`

**Wann:** Bei jeder Feldänderung in der Form, je Feld  
**Auf dem Pad:** ret = super(); switch (_fieldId) { case fieldNum(T, F): ret = ret && this.checkXyz(); } – Prüfung je Feld

Läuft nach jeder Feldänderung in der Form, pro Feld. ret = super() macht die Standardprüfung (Pflichtfeld, Relation); dahinter ein switch über das Feld mit eigener Prüfung. Der Rückgabewert false lässt das Feld rot.

```xpp
public boolean validateField(FieldId _fieldId)
{
    boolean ret = super();
    switch (_fieldId)
    {
        case fieldNum(TariffLine, DateTo):
            ret = ret && this.checkDateRange();
            break;
    }
    return ret;
}
```

### `validateWrite()`

**Wann:** Vor insert / update aus der Form – nicht aus Code  
**Auf dem Pad:** ret = super() – Pflichtfelder sind geprüft; dann Konsistenz über mehrere Felder, checkFailed("…")

Vor insert und update – aber nur, wenn über die Form gespeichert wird. Aus Code muss man validateWrite selbst aufrufen. super() prüft Pflichtfelder; dahinter Prüfungen über mehrere Felder mit checkFailed.

### `validateDelete()`

**Wann:** Vor delete aus der Form  
**Auf dem Pad:** ret = super(); eigene Bedingung – z. B. gebuchte oder abgerechnete Sätze sperren

Vor delete aus der Form. ret = super() prüft die Delete Actions (Restricted); dahinter eigene Regeln, etwa gebuchte oder abgerechnete Sätze sperren.

### `insert()`

**Wann:** Der Datensatz wird geschrieben; RecId wird vergeben  
**Auf dem Pad:** Vor super(): Felder final setzen (Nummernkreis, Zeitstempel). Nach super(): abhängige Sätze anlegen

Schreibt den Satz; super() vergibt die RecId. Felder, die vor dem Schreiben feststehen müssen (Nummernkreis, Zeitstempel), setzt man davor; abhängige Sätze legt man danach an, weil erst dann die RecId bekannt ist.

```xpp
public void insert()
{
    if (!this.OrderId)
        this.OrderId = NumberSeq::newGetNum(MyParameters::numRefOrderId()).num();
    super();
    SalesLine::createFirstStep(this);   // braucht this.RecId
}
```

### `update()`

**Wann:** Eine Änderung wird geschrieben  
**Auf dem Pad:** Vor super(): abhängige Felder nachziehen; nach super(): Folgeaktionen – this.orig() liefert den alten Stand

Schreibt eine Änderung. Vor super() abhängige Felder nachziehen; nach super() Folgeaktionen. this.orig() liefert den Zustand vor der Änderung – praktisch, um zu sehen, was sich geändert hat.

```xpp
public void update()
{
    if (this.Status != this.orig().Status)
        MyEventLog::write(this, "Status geändert");
    super();
}
```

### `delete()`

**Wann:** Der Datensatz wird gelöscht, Cascade läuft mit  
**Auf dem Pad:** Vor super(): Prüfung; nach super(): aufräumen, was keine Delete Action abdeckt

Löscht den Satz; super() führt die Cascade-Delete-Actions aus. Prüfungen davor, Aufräumen danach – zum Beispiel Sätze, die keine Delete Action abdeckt.

### `modifiedField(_fieldId)`

**Wann:** Nach einer Feldänderung in der Form  
**Auf dem Pad:** switch (_fieldId) – abhängige Felder desselben Satzes setzen (Preis nach Menge, Adresse nach Kunde)

Nach einer Feldänderung in der Form (nach validateField). Hier setzt man abhängige Felder desselben Satzes: Preis nach Menge, Adresse nach Kunde. Ein switch über _fieldId wie bei validateField.

```xpp
public void modifiedField(FieldId _fieldId)
{
    super(_fieldId);
    switch (_fieldId)
    {
        case fieldNum(TariffLine, Qty):
            this.Amount = this.Qty * this.Price;
            break;
    }
}
```

## Verknüpft

- [Alle Blöcke](../README.md)
