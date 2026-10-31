# Controls und Form im Code

> **Pad-Block „Controls und Form im Code“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 1 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *element = diese Form · Ctrl = Name des Steuerelements aus dem Designer*

### `ctrl.visible(false); ctrl.enabled(false);`

**Auf dem Pad:** verstecken / sperren

Ein Control ausblenden oder sperren. Das Control heißt im Code wie im Designer, wenn AutoDeclaration = Yes gesetzt ist.

### `ctrl.text("…"); ctrl.value(x);`

**Auf dem Pad:** Text / Wert lesen oder setzen

Text lesen oder setzen bei String-Controls; value() bei allem anderen (Zahl, Datum, Enum, Checkbox).

### `ctrl.mandatory(true); ctrl.allowEdit(false);`

**Auf dem Pad:** Pflichtfeld / schreibgeschützt

Pflichtfeld-Markierung und Schreibschutz für ein einzelnes Control.

### `element.design().controlName("Btn")`

**Auf dem Pad:** Control über seinen Namen holen

Ein Control über seinen Namen holen, wenn es keine AutoDeclaration hat – liefert FormControl, bei Bedarf casten.

### `new MenuFunction(menuItemDisplayStr(F), MenuItemType::Display).run(args);`

**Auf dem Pad:** andere Form über ihr Menu Item öffnen

Eine andere Form über ihr Display Menu Item öffnen, mit Args als Parameter. MenuItemType::Action für Klassen, Output für Reports.

```xpp
Args a = new Args();
a.record(SalesTable);
a.caller(this);
new MenuFunction(menuItemDisplayStr(SalesTable), MenuItemType::Display).run(a);
```

### `fr = mf.create(args); fr.run(); fr.wait(); fr.closedOk()`

**Auf dem Pad:** öffnen, warten, dann abfragen, ob mit OK geschlossen

Wenn man die Form nach dem Schließen abfragen will: create liefert das FormRun-Objekt, run öffnet, wait blockiert bis zum Schließen, closedOk() sagt, ob der Benutzer OK gedrückt hat.

### `Args a = new Args(); a.record(t); a.caller(this);`

**Auf dem Pad:** Parameter für die Ziel-Form

Das Parameterobjekt für Forms und Klassen: record ist der Datensatz, caller das aufrufende Objekt, parm ein Text, parmEnum ein Enum-Wert.

## Verknüpft

- [Alle Blöcke](../README.md)
