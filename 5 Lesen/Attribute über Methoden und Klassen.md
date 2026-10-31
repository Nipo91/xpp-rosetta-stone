# Attribute über Methoden und Klassen

> **Pad-Block „Attribute über Methoden und Klassen“, Familie Lesen**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 1 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *[Attribut] steht über Methode oder Klasse und sagt dem System, wofür sie da ist*

### `[ExtensionOf(tableStr(X))]`

**Auf dem Pad:** Klasse erweitert X per Chain of Command

Die Klasse erweitert X per Chain of Command: gleichnamige Methoden umhüllen die Originale, next ruft sie.

### `[DataContract] / [DataMember]`

**Auf dem Pad:** Parameterklasse / ihr Feld (SysOperation)

SysOperation: Die Klasse ist ein Datenvertrag, die Methode ein Parameter davon.

### `[SRSReportDataSet(…)] / [SRSReportParameter(…)]`

**Auf dem Pad:** SSRS: Datenquelle / Parameter des Reports (läuft aus)

SSRS-Reports: Datenquelle und Parameter einer Report-Data-Provider-Klasse. Bei das Team läuft SSRS aus, taucht im alten Code aber noch auf.

### `[FormProperty(…)] / [FormDesignProperty(…)]`

**Auf dem Pad:** Form-Eigenschaft aus Code setzen

Eigenschaften von Form-Controls aus Code setzen, etwa in Form-Erweiterungen.

### `[SysEntryPoint]`

**Auf dem Pad:** Von außen aufrufbar, Sicherheitsprüfung

Die Methode ist von außen aufrufbar (Service, OData) und läuft mit Sicherheitsprüfung.

## Verknüpft

- [Alle Blöcke](../README.md)
