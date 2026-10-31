# Intrinsische Funktionen

> **Pad-Block „Intrinsische Funktionen“, Familie Lesen**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 1 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Name oder ID zur Compilezeit: Tippfehler fallen beim Bauen auf, Umbenennungen ziehen mit.*

### `tableNum(T) / tableStr(T)`

**Auf dem Pad:** Tabellen-ID / -Name

Liefern ID oder Namen zur Compilezeit: Tippfehler fallen beim Bauen auf, Umbenennungen ziehen mit. Nie den Namen als Text schreiben.

### `fieldNum(T, F) / fieldStr(T, F)`

**Auf dem Pad:** Feld-ID / -Name

Feld-ID und Feldname – in jeder Range und jedem validateField.

### `formStr(F)`

**Auf dem Pad:** Formularname

Formularname, etwa für MenuFunction oder Form-Erweiterungen.

### `enumStr(E) / enumCum(E, Wert)`

**Auf dem Pad:** Enum-Name / Element als Zahl

enumStr liefert den Enum-Namen, enumCum den Wert eines Elements als Zahl.

### `classStr(C) / classNum(C) / methodStr(C, m)`

**Auf dem Pad:** Klasse als Name / ID, Methode als Name – so startet SysOperation

classStr liefert den Klassennamen als Text, classNum die ID, methodStr den Methodennamen – alle vom Compiler geprüft. So startet jeder SysOperation-Controller seinen Service.

```xpp
SysOperationServiceController controller = new SysOperationServiceController(
    classStr(MyBillingService), methodStr(MyBillingService, process));
controller.startOperation();
```

### `menuItemDisplayStr(M) / queryStr(Q)`

**Auf dem Pad:** Menüpunkt bzw. AOT-Query aus Code aufrufen

menuItemDisplayStr liefert den Namen eines Display-Menüpunkts (öffnet eine Form), queryStr den Namen einer AOT-Query – beide zum Aufrufen aus Code.

```xpp
new MenuFunction(menuItemDisplayStr(SalesTable), MenuItemType::Display).run(args);
Query q = new Query(queryStr(MyOpenOrders));
```

## Verknüpft

- [Alle Blöcke](../README.md)
