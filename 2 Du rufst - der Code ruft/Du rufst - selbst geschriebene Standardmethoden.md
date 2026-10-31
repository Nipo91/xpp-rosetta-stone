# Du rufst: selbst geschriebene Standardmethoden

> **Pad-Block „Du rufst: selbst geschriebene Standardmethoden“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 3 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Das System ruft keine davon – eigener Code schon.*

### `@02339.Call(9116777)`

**Auf dem Pad:** Number 10 or 30

Easter Egg, kein X++: Du rufst – und wer die Nummer kennt, weiß Bescheid. Nummer 10 oder 30.

### `find(_id, [_forUpdate])`

**Auf dem Pad:** Datensatz zum Schlüssel holen (select firstonly)

Die statische Standardsuche jeder Tabelle: select firstonly über den Primärschlüssel. Mit _forUpdate = true sperrt sie den Satz zum Ändern (nur innerhalb ttsBegin/ttsCommit).

```xpp
public static TariffTable find(TariffId _id, boolean _forUpdate = false)
{
    TariffTable tariff;
    tariff.selectForUpdate(_forUpdate);
    select firstonly tariff where tariff.TariffId == _id;
    return tariff;
}
```

### `findByRecId(_recId)`

**Auf dem Pad:** Datensatz über die RecId holen

Dasselbe über die RecId – praktisch, wenn man nur die RecId hat (Args, Referenzen, Nummern aus Logs).

### `findOrCreate(…)`

**Auf dem Pad:** holen, sonst anlegen

Holt den Satz oder legt ihn an, wenn er fehlt. Typisch für Stammdaten, die beim ersten Zugriff entstehen dürfen. Innen: find, wenn leer insert, dann zurückgeben.

### `initFrom<Tabelle>(_buffer)`

**Auf dem Pad:** eigenen Puffer aus anderem Datensatz füllen

Füllt den eigenen Puffer aus einem anderen Datensatz, Feld für Feld. So kommen Werte vom Auftrag in die Abrechnungszeile.

```xpp
public void initFromTransportOrderTable(SalesTable _order)
{
    this.OrderId   = _order.OrderId;
    this.CustAccount = _order.CustAccount;
}
```

### `display<Xyz>()`

**Auf dem Pad:** berechnete Spalte fürs Grid, nicht gespeichert

Eine berechnete Spalte für Grids: Die Methode liefert einen Wert, der nicht gespeichert wird. Deklaration mit display vor dem Rückgabetyp; im Grid wird das Control an die Methode gebunden.

```xpp
display PartyName displayPartyName()
{
    return DirPartyTable::findRec(this.Party).Name;
}
```

### `static construct() / new()`

**Auf dem Pad:** Objekt erzeugen statt new direkt / Konstruktor

Objekte werden nicht direkt mit new erzeugt, sondern über construct() – eine Fabrikmethode, die später auch eine Unterklasse zurückgeben kann. new() ist der Konstruktor, oft protected.

```xpp
public static MyBillingLogic construct()
{
    return new MyBillingLogic();
}
```

### `static main(Args _args)`

**Auf dem Pad:** Einstieg vom Menu Item: construct, prompt, run

Der Einstieg, wenn eine Klasse über ein Menu Item gestartet wird: Objekt bauen, Args übergeben, Dialog zeigen, laufen lassen.

```xpp
public static void main(Args _args)
{
    MyBillingJob job = MyBillingJob::construct();
    job.parmRecord(_args.record());
    if (job.prompt()) job.run();
}
```

### `initQuery()`

**Auf dem Pad:** Query des Laufs aufbauen

Baut die Query eines Laufs auf, meist mit Ranges aus den Dialogwerten. Wird von RunBase-Klassen aus run() oder queryRun() gerufen.

### `parm<Xyz>(_v = v)`

**Auf dem Pad:** lesen ohne Argument, setzen mit Argument

Getter und Setter in einer Methode: ohne Argument lesen, mit Argument setzen. Das Muster ist überall in X++ – Parameter von Klassen, Werte von Dialogen.

```xpp
public SalesId parmOrderId(SalesId _orderId = orderId)
{
    orderId = _orderId;
    return orderId;
}
```

### `getXyz() / setXyz(_v)`

**Auf dem Pad:** Getter und Setter getrennt – in vielen Projekten häufig neben parm; set gibt meist nichts zurück

das Team schreibt daneben oft getrennte Getter und Setter wie in C#: getXyz() liest, setXyz(_v) setzt. Lesen beide gleich: Zugriff auf eine Membervariable, manchmal mit Nebenwirkung im Setter.

## Verknüpft

- [Alle Blöcke](../README.md)
