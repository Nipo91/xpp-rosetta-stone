# System ruft: Data Source

> **Pad-Block „System ruft: Data Source“, Familie System ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 5 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Im Form-Code: CustTable = aktueller Datensatz, CustTable_ds = die Data Source (research, refresh, query()).*

### `init()`

**Wann:** Beim Öffnen aus Form-init; die Query der Data Source entsteht  
**Auf dem Pad:** Nach super(): this.query() anpassen – Ranges, Sortierung, Joins; dynamische Links lösen (clearDynalinks)

super() erzeugt die Query der Data Source aus den Metadaten. Danach kann man sie mit this.query() verändern: Ranges, Sortierung, Joins. Was hier steht, gilt für die ganze Lebenszeit der Form.

```xpp
public void init()
{
    super();
    this.query().dataSourceTable(tableNum(SalesTable))
        .addSortField(fieldNum(SalesTable, CreatedDateTime), SortOrder::Descending);
}
```

### `executeQuery()`

**Wann:** Beim Öffnen und bei jedem research / Filter; die Query läuft  
**Auf dem Pad:** Vor super(): Ranges nach aktuellem Zustand setzen (Checkbox, Args); danach sind die Daten frisch

Läuft beim Öffnen und bei jedem research() oder Filter. Ranges, die vom aktuellen Zustand abhängen (eine Checkbox, ein Datum), setzt man vor super(), dann liefert die Query sofort das Richtige.

```xpp
public void executeQuery()
{
    QueryBuildRange r = SysQuery::findOrCreateRange(this.query().dataSourceTable(tableNum(T)), fieldNum(T, Status));
    r.value(ShowAll.value() ? SysQuery::valueUnlimited() : queryValue(MyStatus::Open));
    super();
}
```

### `active()`

**Wann:** Bei jedem Wechsel des aktuellen Datensatzes  
**Auf dem Pad:** Nach super(): Buttons und Felder passend zum Satz schalten (enabled, visible, allowEdit), abhängige Data Sources filtern

Jeder Wechsel des aktuellen Datensatzes – auch der erste beim Öffnen. Nach super() ist der Puffer T gefüllt; jetzt Controls passend schalten (enabled, visible, allowEdit) oder abhängige Data Sources filtern.

```xpp
public int active()
{
    int ret = super();
    BtnPost.enabled(BordereauTable.Status == BordereauStatus::Open);
    return ret;
}
```

### `linkActive()`

**Wann:** Der übergeordnete Datensatz hat gewechselt (Master / Detail)  
**Auf dem Pad:** Vor super(): Ranges der Detail-Query an den neuen Elternsatz anpassen; super() führt die Detail-Query aus

Master/Detail: Wechselt im übergeordneten Grid der Satz, ruft das System im Detail linkActive. super() führt die Detail-Query mit dem neuen Elternsatz aus – eigene Ranges deshalb davor setzen.

### `create()`

**Wann:** Der Benutzer legt einen neuen Datensatz an  
**Auf dem Pad:** Nach super(): Werte aus dem Kontext setzen (Elternschlüssel, Args), die gespeichert bleiben sollen

Der Benutzer drückt Neu (oder Ctrl+N). super() legt den leeren Puffer an; danach Werte setzen, die aus dem Kontext kommen – etwa der Schlüssel des Elternsatzes oder ein Wert aus den Args.

### `initValue()`

**Wann:** Beim Neuanlegen, nach create; ruft initValue der Tabelle  
**Auf dem Pad:** Nach super(): Vorbelegungen, die nur in dieser Form gelten; zählt nicht als Änderung

Läuft nach create und ruft initValue der Tabelle. Was nur in dieser Form vorbelegt werden soll, kommt hinter super(); die Vorbelegung zählt nicht als Änderung, der Satz bleibt „neu“.

### `validateWrite()`

**Wann:** Vor dem Speichern, nach validateWrite der Tabelle  
**Auf dem Pad:** ret = super(); dann formularspezifische Prüfung mit checkFailed; false verhindert das Speichern

Vor dem Speichern, boolean. ret = super() prüft Pflichtfelder und ruft validateWrite der Tabelle. Eine Prüfung, die nur in dieser Form gilt, hängt man dahinter – false verhindert das Speichern.

```xpp
public boolean validateWrite()
{
    boolean ret = super();
    if (ret && TariffLine.Amount <= 0)
        ret = checkFailed("Der Betrag muss größer als 0 sein.");
    return ret;
}
```

### `write()`

**Wann:** Beim Speichern: validateWrite, dann insert / update der Tabelle  
**Auf dem Pad:** Nach super(): abhängige Sätze schreiben, andere Data Sources neu laden (research), Meldung ausgeben

super() macht validateWrite und dann insert oder update der Tabelle. Danach läuft, was nach dem Speichern passieren soll: abhängige Sätze schreiben, andere Data Sources neu laden, eine Meldung.

### `validateDelete() / delete()`

**Wann:** Beim Löschen: Rückfrage, dann Löschen  
**Auf dem Pad:** validateDelete: eigene Bedingung statt der Standard-Rückfrage. delete: nach super() abhängige Sätze oder Anzeige nachziehen

validateDelete entscheidet, ob gelöscht werden darf – der Standard fragt den Benutzer; eine eigene Prüfung ersetzt das. delete löscht über die Tabelle; nach super() aufräumen, was die Delete Actions nicht abdecken.

### `research(true) / reread() / refresh()`

**Wann:** Nur aus eigenem Code aufgerufen  
**Auf dem Pad:** research(true): Query neu, Position halten · reread: Satz aus der DB neu lesen · refresh: nur Anzeige erneuern

Drei Stufen, immer aus eigenem Code: research(true) führt die Query neu aus und hält die Position im Grid; reread liest nur den aktuellen Satz neu aus der Datenbank; refresh zeichnet die Anzeige neu, ohne Datenbankzugriff.

```xpp
SalesTable_ds.research(true);   // nach einem Batch, der Sätze geändert hat
SalesTable_ds.reread();         // nach einem update() auf dem Puffer
SalesTable_ds.refresh();        // nach einer Feldänderung im Puffer
```

## Verknüpft

- [Alle Blöcke](../README.md)
