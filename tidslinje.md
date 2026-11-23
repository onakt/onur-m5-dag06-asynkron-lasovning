# Tidslinje: rita vad som händer

Välj snutt 5 och snutt 10. Fyll i tabellerna steg för steg. Skriv vad som ligger i varje del **efter** varje steg.

Förklaring:

- **Anropsstacken** är den kod som körs just nu.
- **Microtask-kön** är promise-callbacks som väntar på att få köra.
- **Task-kön** är timer-callbacks och liknande som väntar på att få köra.
- Regel: när stacken är tom körs först ALLA microtasks, sedan EN task, sedan tomma microtasks igen, och så vidare.

## Snutt 5

| Steg | Vad händer | Stacken | Microtask-kön | Task-kön | Utskrift hittills |
|---|---|---|---|---|---|
| 1 | setTimeout anropas |setTimeout(...)| |skriv timeout|–|
| 2 | Promise.resolve().then(...) anropas |Promise (anrop)|skriv promise|skriv timeout|–|
| 3 | console.log("sync") |skriv sync|skriv promise|skriv timeout|sync|
| 4 | Stacken tom: vad körs först? |promise först|–|skriv timeout|sync, promise|
| 5 | Nästa |timeout|–|–|sync, promise, timeout|

## Snutt 10

| Steg | Vad händer | Stacken | Microtask-kön | Task-kön | Utskrift hittills |
|---|---|---|---|---|---|
| 1 | console.log("1") |skriv 1|–|–|1|
| 2 | första setTimeout |setTimeout(...)|–|skriv 2|1|
| 3 | Promise.resolve().then(3) |Promise|skriv 3|skriv 2|1|
| 4 | andra setTimeout |setTimeout(...)|skriv 3|skriv 2, 4 + Promise.then("5")|1|
| 5 | console.log("6") |skriv 6|skriv 3|skriv 2, 4 + Promise.then("5")|1, 6|
| 6 | stacken tom, microtask-kön först |skriv 3|–|skriv 2, 4 + Promise.then("5")|1, 6, 3|
| 7 | första tasken |skriv 2|–|skriv 4 + Promise.then("5")|1, 6, 3, 2|
| 8 | andra tasken |skriv 4, Promise.then("5")|skriv 5|–|1, 6, 3, 2, 4|
| 9 | microtask 5 |skriv 5|–|–|1, 6, 3, 2, 4, 5|

## Min förklaring i en mening

Varför kommer en promise-callback före en timer med 0 ms?
För att promise-callback hamnar i microtask-kön medan timer-callbacks hamnar i task-kön. Regeln är att när stacken är tom så körs först ALLA microtasks, sedan EN task, sedan tomma microtasks igen, och så vidare. Därför kommer promise-callback före en timer, även om den har 0 ms.