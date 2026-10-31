# Container, List, Map, Set

> **Pad-Block „Container, List, Map, Set“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 3 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *container = Werteliste ohne Typ, jede Änderung = Kopie · List = List<T> · Map = Dictionary · Set = HashSet · durchlaufen mit Enumerator: moveNext() / current()*

### `[a, b] = c`

**Auf dem Pad:** Container in Variablen zerlegen: a = 1. Wert, b = 2.

Container zerlegen: die ersten Elemente in Variablen – so liest unpack den gespeicherten Zustand.

### `c += [x]`

**Auf dem Pad:** Wert anhängen – erzeugt eine neue Kopie

Anhängen; Container sind unveränderlich, += erzeugt einen neuen.

### `conPeek(c, 1) / conLen(c)`

**Auf dem Pad:** Element 1 lesen (zählt ab 1) / Anzahl der Elemente

conPeek liest Element 1 (Zählung ab 1), conLen die Länge. conIns fügt ein, conDel löscht.

### `for (i = 1; i <= conLen(c); i++) x = conPeek(c, i);`

**Auf dem Pad:** Container durchlaufen – zählt ab 1

Container haben keinen Enumerator: Schleife mit Zähler von 1 bis conLen(c), jedes Element mit conPeek(c, i) lesen. Zählung ab 1, nicht ab 0 wie in C#.

```xpp
for (i = 1; i <= conLen(c); i++)
    info(strFmt("%1", conPeek(c, i)));
```

### `List l = new List(Types::String)`

**Auf dem Pad:** Liste, alle Elemente vom Typ String (C#: List<T>)

Eine Liste mit festem Elementtyp (Types::String, Types::Record, Types::Class).

### `l.addEnd(x) / l.elements()`

**Auf dem Pad:** hinten anhängen / Anzahl

addEnd hängt an, elements() zählt. Durchlaufen mit getEnumerator / moveNext / current.

### `ListEnumerator e = l.getEnumerator(); while (e.moveNext()) e.current()`

**Auf dem Pad:** List durchlaufen; Set genauso (SetEnumerator)

Kein foreach in X++: getEnumerator() liefert den Enumerator, moveNext() schaltet weiter und liefert false am Ende, current() gibt das aktuelle Element. Set genauso, mit SetEnumerator.

```xpp
ListEnumerator e = l.getEnumerator();
while (e.moveNext())
    info(e.current());
```

### `Map m = new Map(Types::String, Types::Real)`

**Auf dem Pad:** Schlüssel → Wert, Typen für beides (C#: Dictionary)

Schlüssel-Wert-Paare mit festen Typen; Set dagegen nur eindeutige Werte (s.add, s.in).

### `m.insert(k, v) / m.lookup(k) / m.exists(k)`

**Auf dem Pad:** Wert setzen / Wert zum Schlüssel holen / gibt es den Schlüssel?

insert legt an oder überschreibt, lookup liest (Fehler, wenn der Schlüssel fehlt – deshalb vorher exists).

### `MapEnumerator me = m.getEnumerator()`

**Auf dem Pad:** Map durchlaufen wie List: while (me.moveNext()) me.currentKey() / me.currentValue()

Wie bei List, nur hat der Enumerator zwei Werte: currentKey() und currentValue().

```xpp
MapEnumerator me = m.getEnumerator();
while (me.moveNext())
    info(strFmt("%1: %2", me.currentKey(), me.currentValue()));
```

### `Set s = new Set(Types::Integer); s.add(x); s.in(x)`

**Auf dem Pad:** Menge: jeder Wert nur einmal / hinzufügen / enthalten?

Set = Menge ohne Doppelte: add(x) fügt hinzu (ein zweites Mal wird still ignoriert), in(x) prüft, ob enthalten. Praktisch gegen Dubletten, z. B. für schon verarbeitete RecIds.

```xpp
Set done = new Set(Types::Int64);
if (!done.in(order.RecId))
{
    done.add(order.RecId);
    this.process(order);
}
```

## Verknüpft

- [Alle Blöcke](../README.md)
