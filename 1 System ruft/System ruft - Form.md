# System ruft: Form

> **Pad-Block „System ruft: Form“, Familie System ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 3 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Öffnen: new → init → run → executeQuery → active. Schließen: closeOk → canClose → close.*

### `init()`

**Wann:** Beim Öffnen, nach new – Form und Data Sources entstehen  
**Auf dem Pad:** Vor super(): Args prüfen (element.args().record(), parm). Nach super(): Controls holen, Ranges setzen, Variablen vorbelegen

Das System ruft init() genau einmal beim Öffnen. super() baut die Form auf – Design, Controls, Data Sources. Was Args prüft, gehört davor; was Controls oder Data Sources anfasst, dahinter, weil es sie vorher noch nicht gibt.

```xpp
public void init()
{
    if (!element.args().record())
        throw error("Diese Form braucht einen Datensatz.");
    super();
    tariffId = element.args().record().RecId;
    TariffLine_ds.query().dataSourceTable(tableNum(TariffLine))
        .addRange(fieldNum(TariffLine, TariffTable)).value(queryValue(tariffId));
}
```

### `run()`

**Wann:** Nach init; das Fenster erscheint, die Queries laufen  
**Auf dem Pad:** Nach super(): Felder und Buttons je nach Modus ein- / ausschalten, Fokus setzen, Titel anpassen

run() zeigt das Fenster und führt die Queries der Data Sources aus. Nach super() stehen die Daten – jetzt Controls je nach Modus schalten, den Fokus setzen oder den Titel anpassen.

```xpp
public void run()
{
    super();
    this.enableButtons();          // eigene Methode, schaltet nach Status
    BtnRelease.enabled(element.args().openMode() != OpenMode::View);
}
```

### `canClose()`

**Wann:** Vor dem Schließen, vom System gefragt  
**Auf dem Pad:** ret = super(); dann eigene Bedingung – ungespeicherte Eingaben, Pflichtangaben; return false hält die Form offen

Wird vor jedem Schließen gefragt und liefert boolean. ret = super() übernimmt die Standardprüfung (ungespeicherte Änderungen); eine eigene Bedingung hängt man dahinter. return false hält die Form offen.

```xpp
public boolean canClose()
{
    boolean ret = super();
    if (ret && !this.allLinesValid())
    {
        ret = checkFailed("Es gibt noch Zeilen ohne Tarif.");
    }
    return ret;
}
```

### `close()`

**Wann:** Beim Schließen, nach canClose  
**Auf dem Pad:** Aufräumen: Caches leeren, Flags zurücksetzen, Rückgabewerte für den Aufrufer setzen; danach super()

Läuft nach canClose, super() schließt die Form wirklich. Vorher aufräumen: Caches leeren, Flags zurücksetzen, Werte für den Aufrufer bereitstellen.

### `closeOk() / closeCancel()`

**Wann:** OK- bzw. Abbrechen-Knopf; rufen danach close  
**Auf dem Pad:** In Dialog-Forms: Eingaben prüfen und in Variablen übernehmen, dann super(); der Aufrufer liest sie über closedOk()

Die OK- und Abbrechen-Buttons einer Dialog-Form. closeOk merkt sich „mit OK geschlossen“ (closedOk() liefert danach true) und ruft close. Eingaben vorher in Variablen sichern, der Aufrufer liest sie nach fr.wait() über eigene parm-Methoden.

```xpp
public void closeOk()
{
    selectedDate = DateFrom.dateValue();   // Dialogwert sichern
    super();
}
```

### `pageActivated()`

**Wann:** Eine Tab-Seite wird aktiv  
**Auf dem Pad:** Daten dieser Seite erst jetzt laden (Data Source research), teure Berechnungen hierhin verschieben

Wird gerufen, wenn der Benutzer eine Tab-Seite öffnet. Daten, die nur dort gebraucht werden, erst hier laden – spart Zeit beim Öffnen der Form.

```xpp
public void pageActivated()
{
    super();
    if (!historyLoaded)
    {
        MyEventHistory_ds.research();
        historyLoaded = true;
    }
}
```

## Verknüpft

- [Alle Blöcke](../README.md)
