# RunBaseBatch: ein Lauf von main bis run

> **Pad-Block „RunBaseBatch: ein Lauf von main bis run“, Familie Abläufe**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 4 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Ablauf: main → construct → prompt (dialog → getFromDialog → validate) → run.*

### `main(Args) → construct()`

**Wann:** Einstieg vom Menu Item  
**Auf dem Pad:** Objekt erzeugen, Args übergeben (parmRecord), dann prompt() und run()

Der Einstieg vom Menu Item: Objekt über construct bauen, Args übernehmen (parmRecord), prompt() zeigt den Dialog, run() macht die Arbeit.

```xpp
public static void main(Args _args)
{
    MyBillingJob job = MyBillingJob::construct();
    if (job.prompt())
        job.run();
}
```

### `prompt() → dialog()`

**Wann:** Vor run; der Dialog wird aufgebaut  
**Auf dem Pad:** dialog = super(); dialogField = dialog.addField(extendedTypeStr(…), "@…"); Felder vorbelegen

prompt() baut den Dialog auf und ruft dabei dialog(): super() liefert das DialogRunbase-Objekt, jedes Eingabefeld kommt mit addField dazu.

```xpp
public Object dialog()
{
    DialogRunbase dlg = super();
    dlgFromDate = dlg.addField(extendedTypeStr(TransDate), "@ACS:FromDate");
    dlgFromDate.value(fromDate);
    return dlg;
}
```

### `initParmDefault()`

**Wann:** Wenn keine gespeicherten Werte vorliegen  
**Auf dem Pad:** Standardwerte der Variablen setzen (Datum heute, Firma, Parameter)

Wird gerufen, wenn es noch keine gespeicherten Dialogwerte gibt (SysLastValue). Hier Standardwerte setzen: Datum heute, aktuelle Firma.

### `getFromDialog()`

**Wann:** Nach OK im Dialog  
**Auf dem Pad:** ret = super(); variable = dialogField.value(); – jedes Dialogfeld in seine Variable

Nach OK: ret = super(), dann jeden Dialogwert in seine Variable übernehmen – fromDate = dlgFromDate.value().

### `dialogPostRun() / dialogSelectCtrl()`

**Wann:** Nach dem Anzeigen / bei Feldänderung im Dialog  
**Auf dem Pad:** Lookups registrieren (controlMethodOverload(true) am FormRun des Dialogs) / abhängige Felder schalten

dialogPostRun läuft, nachdem der Dialog angezeigt ist – hier registriert man Lookups auf Dialogfeldern. dialogSelectCtrl läuft bei jeder Feldänderung im Dialog, wenn allowUpdateOnSelectCtrl true ist: abhängige Felder schalten.

### `validate()`

**Wann:** Nach getFromDialog, vor run  
**Auf dem Pad:** ret = super(); Werte prüfen, bei Fehler checkFailed; false bricht den Lauf ab

Prüft die Werte nach getFromDialog und vor run. ret = super(); eigene Prüfung mit checkFailed; false bricht den Lauf mit Meldung ab.

### `run()`

**Wann:** Die eigentliche Arbeit; im Batch vom Batch-Server gerufen  
**Auf dem Pad:** ttsBegin … ttsCommit, Fortschritt (progress), info am Ende; keine Dialoge im Batch

Die eigentliche Arbeit – interaktiv und im Batch dieselbe Methode. Transaktion mit ttsBegin/ttsCommit, Fortschritt über progress, am Ende eine info. Keine Dialoge: Im Batch gibt es keinen Benutzer.

```xpp
public void run()
{
    ttsBegin;
    this.processOrders();
    ttsCommit;
    info(strFmt("@ACS:OrdersBilled", counter));
}
```

### `pack() / unpack()`

**Wann:** Beim Speichern des Zustands (SysLastValue, Batch)  
**Auf dem Pad:** #define.CurrentVersion(1) #localmacro.CurrentList variable1, variable2 #endmacro – jede Variable in die Liste

Der Zustand des Objekts als Container – so werden Dialogwerte gespeichert (SysLastValue) und der Lauf an den Batch-Server übergeben. Jede Variable gehört in die CurrentList.

```xpp
#define.CurrentVersion(1)
#localmacro.CurrentList
    fromDate,
    custAccount
#endmacro

public container pack()
{
    return [#CurrentVersion, #CurrentList];
}

public boolean unpack(container _packedClass)
{
    Version version = RunBase::getVersion(_packedClass);
    switch (version)
    {
        case #CurrentVersion:
            [version, #CurrentList] = _packedClass;
            break;
        default:
            return false;
    }
    return true;
}
```

### `canGoBatch() / showBatchTab()`

**Wann:** Beim Dialogaufbau  
**Auf dem Pad:** return true – das Batch-Register erscheint; false für reine Dialogklassen

canGoBatch() true erlaubt den Lauf im Batch; showBatchTab() true zeigt das Batch-Register im Dialog. Reine Dialogklassen geben false zurück.

### `showQueryValues() / queryRun()`

**Wann:** Dialog mit Query-Auswahl  
**Auf dem Pad:** showQueryValues: true → Select-Button; queryRun: eigenes QueryRun zurückgeben, das run() benutzt

showQueryValues() true zeigt die Query-Auswahl und den Select-Button im Dialog; queryRun() liefert das QueryRun, das run() dann durchläuft.

## Verknüpft

- [Alle Blöcke](../README.md)
