# ReadME

## Anleitung
1. Repository entweder downloaden oder klonen mit dieser URL: https://github.com/ct26m044/soloassignment1.git
2. Den Projektordner im Terminal öffnen und mit "npm install" die Abhängigkeiten installieren.
3. Den localhost-Server mit "npm run dev" starten.
4. Den localhost Link im Browser öffnen "https://localhost:####"

## Begründung der Struktur
Die Logik liegt in den Composables "useNotes" und "useLocalStorage", damit die Komponenten nur für die Darstellung zuständig sind. Damit kann jede Datei genau eine Aufgabe übernehmen und ist für diese verantwortlich. Und der localStorage Zugriff ist nur an einer einzigen Stelle anstatt überall.

## Reflexionsfragen
### Warum darf NoteCard die Notiz-Prop nicht selbst verändern, und wie löst ihr das stattdessen?
App.vue ist der Besitzer und dort wird useNotes() aufgerufen. Wenn aber NoteCard dann die Prop selbst verändern würde, dann wüsste App.vue nichts davon und es würde an zwei Stellen auseinanderlaufen. Deswegen meldet NoteCard per emit('delete', note.id) nur, dass etwas passieren soll und App.vue entscheidet, ob er das go geben kann.

### Was passiert, wenn zwei Komponenten dasselbe useNotes() aufrufen - teilen sie sich die Notizen oder nicht? Begründet kurz.
Nein sie teilen sich die Notizen nicht automatisch. Jeder Aufruf von useNotes() führt die function neu aus und erzeugt dadurch ein neues ref mit einer eigenen Liste. Beide verwenden den gleichen localStorage, aber die Änderung erscheint nur in der einen Komponente und nicht live in der anderen. Aus diesem Grund rufe ich useNotes() nur einmal in der App.vue auf und gebe die Daten per props und events weiter.

### Wozu dient das Note-Interface, wenn der Cocde auch ohne liefe?
Es dient dazu, dass es wie eine Notiz ausschaut. TypeScript überprüft, ob die Daten, welche zwischen Komponenten weitergegeben werden zu dieser Form passen. Würde es also Fehler geben wie Rechtschreibfehler, würde das früher auffallen anstatt erst im Browser. Bei der Ausführung im Browser ist das Note-Interface nicht nötig.

