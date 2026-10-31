# Meldungen

> **Pad-Block „Meldungen“, Familie Du rufst · der Code ruft**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 1 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *info / warning / error schreiben ins Infolog · throw bricht ab und rollt zurück*

### `info("…")`

**Auf dem Pad:** Hinweis im Infolog

Hinweis im Infolog; warning() dasselbe als Warnung.

### `error("…")`

**Auf dem Pad:** Fehler, Code läuft weiter

Fehler im Infolog, läuft weiter. Erst throw error bricht ab.

### `throw error("…")`

**Auf dem Pad:** Fehler, bricht ab, Rollback

Abbruch mit Meldung und Rollback der Transaktion.

### `checkFailed("…")`

**Auf dem Pad:** Meldung + false (in validate)

Warnung ins Infolog und false zurück – das Standardmuster in validate-Methoden: return checkFailed("…").

### `setPrefix("…")`

**Auf dem Pad:** Überschrift, unter der die nächsten Meldungen im Infolog hängen (Batch)

setPrefix("Text") setzt eine Überschrift, unter die das Infolog alle folgenden Meldungen derselben Methode hängt. In Batch-Läufen üblich, damit man im Protokoll sieht, zu welchem Auftrag eine Meldung gehört.

```xpp
setPrefix(strFmt("Transportauftrag %1", order.TransportOrderId));
info("Abgerechnet.");    // erscheint eingerückt unter der Überschrift
```

### `Box::yesNo("…", DialogButton::No) == DialogButton::Yes`

**Auf dem Pad:** Rückfrage an den Benutzer; Antwort ist der geklickte Knopf

Box::yesNo zeigt eine Rückfrage; der zweite Parameter ist der vorgewählte Knopf. Zurück kommt DialogButton::Yes oder No, daher der Vergleich. Läuft nur im Client – im Batch gibt es niemanden, der klickt.

```xpp
if (Box::yesNo("Auftrag wirklich stornieren?", DialogButton::No) == DialogButton::Yes)
    this.cancelOrder();
```

## Verknüpft

- [Alle Blöcke](../README.md)
