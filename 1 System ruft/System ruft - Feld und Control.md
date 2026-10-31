# System ruft: Feld und Control

> **Pad-Block „System ruft: Feld und Control“, Familie System ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 3 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Gleiche Namen am Data-Source-Feld (gilt für alle Controls des Feldes) und am Control (nur dieses).*

### `clicked()`

**Wann:** Klick auf einen Button  
**Auf dem Pad:** Eigene Aktion; super() führt das Menu Item des Buttons aus – davor Args füllen, danach T_ds.research()

Klick auf einen Button. super() führt das Menu Item des Buttons aus (bei MenuItemButton) – davor Args füllen, danach meist die Data Source neu laden.

```xpp
void clicked()
{
    super();
    SalesTable_ds.research(true);
}
```

### `modified()`

**Wann:** Feld nach Änderung verlassen; löst validateField aus  
**Auf dem Pad:** Nach super(): abhängige Controls oder Data Sources nachziehen, research(true)

Der Benutzer hat den Wert geändert und das Feld verlassen. super() schreibt den Wert in den Puffer und löst validateField und modifiedField der Tabelle aus. Danach Controls oder Data Sources nachziehen.

### `validate()`

**Wann:** Beim Verlassen nach Eingabe; ruft validateField der Tabelle  
**Auf dem Pad:** ret = super(); zusätzliche Prüfung nur für dieses Control

Beim Verlassen nach einer Eingabe, boolean. super() ruft validateField der Tabelle; eine zusätzliche Prüfung nur für dieses eine Control hängt man dahinter.

### `lookup()`

**Wann:** Die Auswahlliste wird geöffnet (Alt+↓)  
**Auf dem Pad:** Eigenes Lookup: SysTableLookup::newParameters(tableNum(T), this) – addLookupfield, Query, performFormLookup(); dann ohne super()

Öffnet die Auswahlliste (Alt+↓). Mit SysTableLookup baut man eine eigene Liste: Tabelle, sichtbare Felder, Query mit Filter. Dann kein super() – sonst erscheint zusätzlich die Standardliste.

```xpp
public void lookup()
{
    SysTableLookup lookup = SysTableLookup::newParameters(tableNum(TariffTable), this);
    Query q = new Query();
    q.addDataSource(tableNum(TariffTable))
     .addRange(fieldNum(TariffTable, Active)).value(queryValue(NoYes::Yes));
    lookup.addLookupfield(fieldNum(TariffTable, TariffId), true);
    lookup.addLookupfield(fieldNum(TariffTable, Name));
    lookup.parmQuery(q);
    lookup.performFormLookup();
}
```

### `jumpRef()`

**Wann:** „Details anzeigen“ auf dem Feld  
**Auf dem Pad:** Eigenes Zielformular öffnen: Args mit record, MenuFunction … run(args); ohne super()

„Details anzeigen“ auf einem Feld. Statt der Standard-Form öffnet man ein eigenes Ziel: Args mit dem Datensatz, dann die Form über ihr Menu Item. Ohne super().

```xpp
public void jumpRef()
{
    Args args = new Args();
    args.record(TariffTable::find(this.valueStr()));
    new MenuFunction(menuItemDisplayStr(TariffTable), MenuItemType::Display).run(args);
}
```

### `selectionChange()`

**Wann:** Auswahl in ComboBox oder ListBox geändert  
**Auf dem Pad:** Abhängige Controls umschalten, Werte nachladen

ComboBox oder ListBox: Der Benutzer hat einen anderen Eintrag gewählt. Abhängige Controls umschalten oder Werte nachladen.

### `enter() / leave()`

**Wann:** Fokus kommt ins Feld / verlässt es  
**Auf dem Pad:** Hinweise und Vorbelegung beim Betreten; Eingabe prüfen beim Verlassen

enter läuft, wenn der Fokus ins Feld kommt, leave beim Verlassen. Beim Betreten Hinweise oder Vorbelegung, beim Verlassen Prüfungen, die nicht über validate laufen sollen.

### `textChange()`

**Wann:** Bei jeder Eingabe im Textfeld  
**Auf dem Pad:** Live-Filter oder Suche: Range setzen und research(), bei Bedarf verzögert

Bei jeder Eingabe im Textfeld, also je Tastendruck. Typisch für eine Live-Suche: Range setzen und research – bei großen Tabellen verzögert, sonst wird es zäh.

## Verknüpft

- [Alle Blöcke](../README.md)
