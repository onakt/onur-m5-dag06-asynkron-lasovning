# Dag 6 · Asynkron kod: läs och förutsäg

*Modul 5, UI/UX & Frontendutveckling (TypeScript), Lexicon IT-Proffs*

## Vad du ska göra idag

Du lär dig förstå **asynkron kod**: kod som körs senare än den står skriven. Idag skriver du nästan ingen kod. Du läser färdiga snuttar med `setTimeout` och promises, **gissar** utskriftsordningen, kör och jämför. Imorgon skriver du själv.

## Bakgrund

Det här är modulens svåraste begrepp, och därför har det en hel dag. Webbläsaren kan inte stå och vänta på att ett svar från internet kommer, för då fryser sidan. Istället säger den "kör det här senare, när svaret kommit". Resultatet är att kod inte alltid körs i den ordning den står skriven. Förstår du det här kan du skriva (och granska) all kod som hämtar data. Förstår du det inte blir allt som kommer härnäst gissningar.

## TypeScript idag: Promise-typer

En `Promise` har en typ som säger vad den ger när den är klar:

```ts
const vanta = (ms: number) => new Promise<void>((resolve) => setTimeout(resolve, ms));        // ger inget värde
const hamta = (ms: number, v: string) => new Promise<string>((resolve) => setTimeout(() => resolve(v), ms)); // ger en string
```

- `Promise<void>` betyder "blir klar, men ger inget värde".
- `Promise<string>` betyder "ger en text när den är klar".
- `Promise.all([...])` får typen av alla delresultaten. Håll musen över och titta.
- Typerna ändrar inte hur koden körs. Snutt 1–11 beter sig exakt som i JavaScript, och det är hela poängen med dagen: förstå i vilken ordning saker händer.

## Så arbetar du (samma som alltid)

1. **Forka** dagens repo på GitHub (*Fork → Create fork*).
2. **Klona din fork:** *Code → HTTPS → kopiera adressen*. I terminalen (Ctrl+ö i VS Code): `git clone <adressen>`. Öppna den nya mappen i VS Code.
3. **Installera verktygen, en gång per repo:** `npm install` i terminalen.
4. **Starta servern:** `npm run dev`. Öppna adressen den skriver ut (oftast `http://localhost:5173/`). Tryck F12 och välj fliken *Console*. Stoppa med Ctrl+C.
5. **Gör uppgiften.** Spara och kontrollera i webbläsaren och Console efter varje steg. Gör en commit efter varje avslutat steg: `git add .` och `git commit -m "Beskriv vad du gjorde"`.
6. **Kontrollera typerna:** `npm run typecheck`. Tyst betyder att alla typer stämmer. Röda understrykningar i VS Code är TypeScript som varnar.
7. **Skicka upp** när du är klar: `git push`.
8. **Lämna in i Microsoft Forms.**

Fastnar du: skriv ner exakt var och vad du försökt (och vilket felmeddelande du fick), och ta det först i nästa handledda pass. Problem med `npm` eller Node? Läs *Elevguide: Node, Vite och TypeScript*.

> Vite tar bara bort typerna och kör koden. Den kontrollerar dem inte. Sidan kan alltså köras trots röda understrykningar.

## Uppgiften steg för steg

### Steg 1. Förbered: öppna sidan och titta på en snutt

Öppna adressen från `npm run dev`. Du ser elva snuttar, var och en med en *Kör*-knapp. Läs snutt 1 och 2 utan att trycka. Öppna `forutsagelser.md`. Du skriver din gissning i tabellen innan du kör.

### Steg 2. Snutt 1–4

Gissa utskriften för snutt 1 till 4 och skriv din gissning i `forutsagelser.md`. Kör sedan varje snutt, skriv in den faktiska utskriften och markera om du hade rätt. För varje snutt du gissat fel på: skriv en regel med egna ord.

### Steg 3. Snutt 5–8

Samma sak för snutt 5 till 8. Snutt 5 och 8 är de som oftast överraskar. Rita gärna på papper.

### Steg 4. Snutt 9–11

Samma sak för snutt 9 till 11. Snutt 11 är en utmaning: ett `then` som returnerar en ny promise.

### Steg 5. Titta på facit och jämför

Öppna inte `facit`-mappen (den är lärarens). Istället: gå igenom dina regler med en kamrat eller i Console. Kör om de snuttar du gissade fel på och förklara högt varför ordningen blir som den blir.

### Steg 6. Rita tidslinjen

Öppna `tidslinje.md`. Fyll i tabellerna för snutt 5 och snutt 10: vad som ligger på anropsstacken, i microtask-kön och i task-kön efter varje steg. Det här är samma modell som läraren ritade på tavlan.

### Steg 7. Tre meningar

Skriv de tre meningarna sist i `forutsagelser.md` med egna ord: vad JavaScript gör med `setTimeout`, de tre tillstånden hos en promise, och när `then` körs.

### Steg 8. Fördjupning (frivillig): din egen vänta-funktion

I `src/egen.ts`: skriv `vanta(ms)` som returnerar en promise som blir klar efter `ms` millisekunder. Det är den enda koden du skriver idag. Testa den i Console.

## Kontrollista: så vet du att du är klar

- [X] Du har fyllt i gissning *före* faktisk utskrift för alla elva snuttar.
- [X] Du har skrivit en regel för varje snutt du gissade fel på.
- [X] Du kan förklara varför en promise-callback körs före en `setTimeout(..., 0)`.
- [X] Du har fyllt i tidslinjen för snutt 5 och 10.
- [X] Du har skrivit de tre meningarna med egna ord.
- [X] Du har gjort minst tre commits.

## Tips om du fastnar

- Fastnar du på en snutt: skriv ner vilka delar som körs direkt (synkront) och vilka som körs senare. Börja med att skriva alla `console.log` som står direkt i filen.
- Tänk: *först* all vanlig kod, *sedan* alla promise-callbacks, *sedan* en timer i taget.
- `setTimeout(f, 0)` betyder inte "nu", det betyder "så snart som möjligt, men efter nuvarande kod".
- Kör inte om snuttar bara för att se svaret. Gissa först, annars lär du dig ingenting.
- Det är helt normalt att gissa fel på hälften. Det är poängen.

## Inlämning

**Deadline: imorgon klockan 09.00.** Allt lämnas in i Microsoft Forms. Du behöver inte redovisa något muntligt.

I formuläret fyller du i:

1. Länk till din fork av det här repot.
2. Reflektion: Vilken snutt överraskade dig mest, och vilken regel skrev du för den? Förklara med egna ord varför JavaScript inte väntar på `setTimeout`. Vad betyder `Promise<string>` för den som anropar en funktion?

## Vill du mer? (frivilligt)

- Skriv en egen snutt där utskriftsordningen är svår att gissa, och låt en kamrat gissa.
- Läs om `async`-funktioner på MDN (vi tar dem imorgon) och försök förutsäga vad `console.log(minFunktion())` skriver för en `async function`.
- Läs om `queueMicrotask` och försök skriva en snutt med den.
