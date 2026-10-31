# super() lesen

> **Pad-Block „super() lesen“, Familie Lesen**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 1 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *super() = der Standard; eigener Code davor / danach; ohne super() ist der Standard ersetzt*

### `super()`

**Auf dem Pad:** Ruft die Microsoft-Fassung derselben Methode

super() ruft die Microsoft-Fassung derselben Methode – das Standardverhalten. Alles, was in der Methode vor super() steht, läuft vor dem Standard, alles danach nach ihm. Beim Lesen ist die Position von super() der wichtigste Anhaltspunkt.

### `Code davor / danach`

**Auf dem Pad:** Standard beeinflussen / Ergebnis nutzen

Code vor super() beeinflusst den Standard (Ranges vor executeQuery, Felder vor insert); Code danach nutzt das Ergebnis (Data Sources nach Form-init, der gefüllte Puffer nach active).

### `ret = super(); if (ret) …`

**Auf dem Pad:** validateWrite, validateField, canClose: Standardprüfung einsammeln

Bei Methoden mit Rückgabe (validateWrite, validateField, canClose) sammelt man das Standardergebnis in ret ein und hängt die eigene Prüfung mit && dahinter. So bleibt die Standardprüfung erhalten.

```xpp
boolean ret = super();
if (ret) ret = this.eigenePruefung();
return ret;
```

### `ohne super()`

**Auf dem Pad:** Nur wenn der Standard bewusst ersetzt wird, z. B. lookup() mit eigener Liste

Fehlt super(), wird der Standard bewusst ersetzt – typisch bei lookup() mit eigener Liste oder jumpRef() mit eigenem Ziel. Beim Lesen: Dann passiert nur, was hier steht.

## Verknüpft

- [Alle Blöcke](../README.md)
