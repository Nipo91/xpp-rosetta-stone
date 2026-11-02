# Git in der Konsole

> **Pad-Block „Git in der Konsole“, Familie Werkzeug**
> Jede Zeile des Blocks, so wie sie auf dem Mauspad steht, mit zwei bis drei Sätzen dazu und einem kurzen Beispiel, wo es hilft. Lesezeit etwa 2 Minuten. Das Pad: X++ Mauspad.
> Fußzeile des Blocks: *Terminal Ctrl+Ö · Git Changes Ctrl+G · → = danach · Icon & Co. stehen nur im XML – .xml mit anhängen*

### `git status`

**Auf dem Pad:** Geändert, gestaged, welcher Branch

Zeigt geänderte und gestagte Dateien und den aktuellen Branch. Erster Blick vor jedem Commit.

### `git switch main → git pull`

**Auf dem Pad:** auf main, aktuellen Stand holen

Auf main wechseln und den aktuellen Stand vom Server holen – der Anfang jeder Änderung in der Praxis.

### `git fetch → git switch VG/28111995`

**Auf dem Pad:** DevOps-Branch holen und wechseln

fetch holt die neuen Branches vom Server (den in DevOps angelegten feature/<PBI>), switch wechselt hinein.

### `git add -p / git add .`

**Auf dem Pad:** Teile stagen / alles stagen

add -p geht die Änderungen stückweise durch und fragt je Stück (y/n) – so kommen nur gewollte Änderungen in den Commit. add . nimmt alles.

### `git restore <Datei>`

**Auf dem Pad:** Änderung verwerfen

Verwirft die Änderung an einer Datei (zurück zum letzten Commit). git restore --staged nimmt sie nur aus dem Staging.

### `git diff / git diff --staged`

**Auf dem Pad:** Änderungen: ungestaged / gestaged

Zeigt die ungestagten Änderungen; --staged die, die schon im nächsten Commit sind.

### `git commit -m "<PBI>: …"`

**Auf dem Pad:** Commit mit Text

Commit mit Text; Das Team hat keine feste Vorgabe, die PBI-Nummer vorne hilft beim Suchen.

### `git push -u origin KGLV/15022026`

**Auf dem Pad:** hochladen, dann PR in DevOps

Lädt den Branch hoch; -u merkt sich die Verbindung, danach reicht git push. Der Pull Request entsteht in DevOps.

### `git stash / git stash pop`

**Auf dem Pad:** beiseitelegen / zurückholen

Änderungen beiseitelegen, um kurz den Branch zu wechseln; pop holt sie zurück.

### `git cherry-pick <hash>`

**Auf dem Pad:** Commit übernehmen (Release-Branch)

Übernimmt einen einzelnen Commit in den aktuellen Branch – der Weg von main in den Release-Branch. Den Hash zeigt git log.

## Verknüpft

- [Alle Blöcke](../README.md)
