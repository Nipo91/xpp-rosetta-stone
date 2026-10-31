# Args lesen

> **Pad-Block „Args lesen“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 1 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *element.args() = Übergabeobjekt des Aufrufers; leer, wenn direkt geöffnet*

### `element.args().record()`

**Auf dem Pad:** übergebener Datensatz

Der Datensatz, mit dem die Form geöffnet wurde (Menu Item aus einem Grid, oder a.record(t) im Code). In init() prüfen und mit as oder über den Tabellentyp verwenden.

```xpp
SalesTable order = element.args().record() as SalesTable;
```

### `args().dataset()`

**Auf dem Pad:** Tabellen-Id dieses Datensatzes

Die Tabellen-ID des übergebenen Datensatzes – nützlich, wenn eine Form von verschiedenen Tabellen aus geöffnet werden kann.

```xpp
if (element.args().dataset() == tableNum(BordereauTable)) { … }
```

### `args().parm()`

**Auf dem Pad:** übergebener Text

Ein frei verwendbarer Text, den der Aufrufer mitgibt (a.parm("Abrechnung")). Für mehr als einen Wert nimmt man parmEnum/parmEnumType oder ein eigenes Parameterobjekt über parmObject.

### `args().caller()`

**Auf dem Pad:** aufrufende Form oder Klasse

Das aufrufende Objekt – die Form oder Klasse, die geöffnet hat. Damit lässt sich zurückrufen, etwa den Aufrufer nach dem Schließen neu laden.

```xpp
if (element.args().caller() is FormRun)
{
    FormRun caller = element.args().caller();
    caller.dataSource().research(true);
}
```

### `args().openMode()`

**Auf dem Pad:** Neu, Bearbeiten, Ansehen

openMode() sagt, wozu die Form geöffnet wurde: OpenMode::New, Edit, View oder Auto. In init() oder run() schaltet man danach Felder und Buttons – im Ansehen-Modus alles schreibgeschützt.

```xpp
if (element.args().openMode() == OpenMode::View)
    SalesTable_ds.allowEdit(false);
```

## Verknüpft

- [Alle Blöcke](../README.md)
