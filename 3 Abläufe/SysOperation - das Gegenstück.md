# SysOperation: das Gegenstück

> **Pad-Block „SysOperation: das Gegenstück“, Familie Abläufe**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 1 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Je Lauf drei Klassen: Contract (Daten) · Service (Arbeit) · Controller (Start, Dialog)*

### `[DataContractAttribute] class …Contract`

**Auf dem Pad:** Parameter des Laufs als Klasse

Der Datenvertrag: eine Klasse, die nur die Parameter des Laufs trägt. SysOperation baut daraus den Dialog automatisch.

### `[DataMemberAttribute] parm<Xyz>()`

**Auf dem Pad:** ein Parameter = eine parm-Methode

Jede parm-Methode mit diesem Attribut wird ein Dialogfeld und ein Parameter des Laufs.

```xpp
[DataContractAttribute]
class MyBillingContract
{
    TransDate fromDate;

    [DataMemberAttribute, SysOperationLabelAttribute(literalStr("@ACS:FromDate"))]
    public TransDate parmFromDate(TransDate _fromDate = fromDate)
    {
        fromDate = _fromDate;
        return fromDate;
    }
}
```

### `class …Service { [SysEntryPoint] … }`

**Auf dem Pad:** die eigentliche Arbeit, erhält den Contract

Der Service macht die Arbeit: eine Methode mit [SysEntryPoint], die den Contract bekommt. Keine Dialoge, keine Formulare.

### `class …Controller extends SysOperationServiceController`

**Auf dem Pad:** startet den Lauf, zeigt Dialog, erlaubt Batch

Der Controller startet den Lauf: zeigt den Dialog, erlaubt Batch, verbindet Service und Contract.

### `static main(Args)`

**Auf dem Pad:** Einstieg: Controller anlegen, startOperation()

Wie bei RunBase: Controller bauen, parmArgs, startOperation() – das übernimmt Dialog, Validierung und Batch-Übergabe.

```xpp
public static void main(Args _args)
{
    MyBillingController c = new MyBillingController(classStr(MyBillingService), methodStr(MyBillingService, process));
    c.parmArgs(_args);
    c.startOperation();
}
```

## Verknüpft

- [Alle Blöcke](../README.md)
