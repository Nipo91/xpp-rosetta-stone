# Syntax lesen

> **Pad-Block „Syntax lesen“, Familie Lesen**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 2 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *:: ohne Objekt (statisch) · . auf einem Objekt · _x Parameter · "@…" Label*

### `this. / element`

**Auf dem Pad:** Eigenes Objekt / das Formular selbst

this ist das eigene Objekt (Klasse, Tabelle, Form-Methode); element ist in Form-Code immer die Form selbst (FormRun).

### `Klasse::m() · Tabelle::find(_id) · Enum::Wert`

**Auf dem Pad:** Zwei Doppelpunkte = statisch, ohne Objekt: static-Methode einer Klasse oder Tabelle, Wert eines Enums (NoYes::Yes, SortOrder::Descending)

Zwei Doppelpunkte heißen „statisch, kein Objekt nötig“: static-Methode einer Klasse oder Tabelle (TariffTable::find), Wert eines Enums (NoYes::Yes, SortOrder::Descending, JoinMode::ExistsJoin).

### `obj.m() · t.Feld`

**Auf dem Pad:** Ein Punkt = auf einem Objekt oder Datensatzpuffer

Ein Punkt heißt „auf einem Objekt oder Puffer“: obj.m() ruft eine Instanzmethode, t.Feld liest ein Feld des Datensatzes.

### `_param`

**Auf dem Pad:** Methodenparameter: Unterstrich = kommt vom Aufrufer, nicht hier angelegt

Unterstrich vorn = Parameter: Der Wert kommt vom Aufrufer in die Methode. Variablen ohne Unterstrich legt die Methode selbst an. Reine Konvention, aber überall eingehalten – beim Lesen zeigt sie sofort, woher ein Wert stammt.

```xpp
public void modifiedField(FieldId _fieldId)   // _fieldId: vom Aufrufer
{
    CustTable custTable;                       // custTable: hier angelegt
    …
}
```

### `"@SYS123"`

**Auf dem Pad:** Label-ID; der Text kommt in der Sprache des Benutzers

Ein Label: Datei und ID. Der Benutzer sieht den Text in seiner Sprache; im Code steht nur die ID. @SYS sind Microsoft-Labels, @MyLabels die Datei.

### `obj as T / obj is T`

**Auf dem Pad:** umwandeln (null, wenn unpassend) / prüfen – args().record() as CustTable

as wandelt in den Typ um und liefert null, wenn es nicht passt; is prüft nur. Typisch bei Args: der übergebene Datensatz ist zunächst nur ein Common.

```xpp
CustTable custTable = element.args().record() as CustTable;
if (custTable)
    custAccount = custTable.AccountNum;
```

## Verknüpft

- [Alle Blöcke](../README.md)
