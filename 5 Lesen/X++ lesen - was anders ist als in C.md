# X++ lesen: was anders ist als in C#

> **Pad-Block „X++ lesen: was anders ist als in C#“, Familie Lesen**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 2 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Operatoren wie C#: && || ! ?: · ungleich: != oder <>, beides gleich · switch nur auf Gleichheit – kein case < 5 wie in C#, dafür if / else if*

### `switch (x) { case 1, 2: … break; }`

**Auf dem Pad:** mehrere Werte je case erlaubt · ohne break läuft es in den nächsten case weiter – C# verbietet das

Ein case darf mehrere Werte haben (case 1, 2:). Ohne break läuft die Ausführung in den nächsten case – anders als in C#, wo das ein Fehler wäre.

### `try { } catch (Exception::Error) { } catch (Exception::CLRError) { }`

**Auf dem Pad:** Fehlerart ist ein Enum, kein Typ: Error = X++-Fehler, CLRError = Fehler aus .NET-Aufrufen

Fehlerarten sind das Enum Exception: Error für normale Fehler, CLRError für Fehler aus .NET-Aufrufen, Deadlock und UpdateConflict für Datenbankkonflikte.

### `retry`

**Auf dem Pad:** im catch: zurück an den Anfang des try – üblich bei Deadlock und UpdateConflict

Springt zurück an den Anfang des try-Blocks – das Muster bei Deadlock und UpdateConflict: Variablen zurücksetzen, retry.

```xpp
try
{
    ttsBegin;
    this.process();
    ttsCommit;
}
catch (Exception::Deadlock)
{
    retry;
}
```

### `where t.Name like "A*"`

**Auf dem Pad:** Textvergleich mit Platzhaltern direkt im select: * beliebig viele Zeichen, ? genau eines

Platzhalter direkt im select: * für beliebig viele Zeichen, ? für genau eins.

### `#define.Name(1) / #Name / #localmacro.Liste … #endmacro`

**Auf dem Pad:** Makro = Textersetzung vor dem Kompilieren: Konstante festlegen / einsetzen / Textblock – das Muster hinter pack und unpack

Makros sind Textersetzung vor dem Kompilieren: #define.Name(1) definiert, #Name setzt ein. #localmacro … #endmacro für mehrzeilige Blöcke – das Muster hinter pack und unpack.

### `crossCompany / changecompany(c) { }`

**Auf dem Pad:** select crossCompany liest über alle Firmen · changecompany wechselt im Block in eine andere Firma

select crossCompany liest über alle Firmen (das Feld dataAreaId sagt, aus welcher). changecompany(c) { … } wechselt im Block in eine Firma.

## Verknüpft

- [Alle Blöcke](../README.md)
