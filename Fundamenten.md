# Fundamenten

# Types

## Variabelen

Variabelen zijn als gelabelde doosjes in je programma waarin je data kunt bewaren. Zie ze als kleine plakbriefjes met een naam erop - je schrijft een waarde op dat briefje, en later kun je via die naam de waarde weer ophalen.

In Java moet je, voordat je een variabele gebruikt, twee dingen aangeven: welk type data erin komt en welke naam je eraan geeft. Dat heet het declareren van een variabele.

Als je bijvoorbeeld iemands leeftijd wilt opslaan, kun je dit schrijven:

```java
int age = 25;
```

Hier betekent `int` een geheel getal, `age` is de naam van je doosje, en `25` is de waarde die je erin stopt.

De naam die je kiest moet beschrijven waarvoor de data dient - dat maakt je code later veel makkelijker leesbaar. Dus in plaats van `x` is `age` of `price` veel beter.

Zie de sectie `Types` als je Java-gereedschapskist: elk type is een ander hulpmiddel voor een andere taak.

# Primitieve Types

Primitieve types zijn de meest basale datatypes van Java. Ze slaan simpele waarden direct op, zoals getallen of waar/onwaar.

Zie primitieve types als de "ingebouwde kleine containers" die Java je geeft voor veelgebruikte data.

Belangrijke primitieve types:

- `byte` - heel kleine gehele getallen
- `short` - kleine gehele getallen
- `int` - normale gehele getallen
- `long` - zeer grote gehele getallen
- `float` - decimale getallen (minder precies)
- `double` - decimale getallen (nauwkeuriger, meest gebruikt voor decimalen)
- `char` - één enkel teken
- `boolean` - `true` of `false`

Voorbeeld:

```java
int age = 25;
double price = 19.99;
boolean isStudent = true;
char grade = 'A';
```

Gebruik primitieve types wanneer je alleen een eenvoudige waarde nodig hebt, zonder extra gedrag.

# Referentie Types

Referentietypes verschillen van primitieve types. In plaats van de echte data direct op te slaan, slaan ze een verwijzing (een adres) op naar waar die data in het geheugen staat.

Je kunt een variabele van een referentietype zien als een briefje waarop staat: "het echte object staat daar."

Veelgebruikte referentietypes zijn:

- `String`
- Arrays (zoals `int[]`)
- Klassen die je zelf maakt (zoals `Person`, `Car`, enz.)

Voorbeeld:

```java
String name = "Stefan";
int[] scores = {90, 85, 100};
```

Zowel `name` als `scores` bevatten verwijzingen naar objecten, niet de ruwe objectdata zelf.

# Primitieve vs Referentie Types

Het grootste verschil zit in hoe waarden worden opgeslagen en gekopieerd.

- Primitieve variabele: slaat de echte waarde op.
- Referentievariabele: slaat het adres van een object op.

Voorbeeld met primitieve types:

```java
int a = 10;
int b = a;
b = 20;
System.out.println(a); // 10
```

`a` blijft `10`, omdat `b` zijn eigen kopie van de waarde kreeg.

Voorbeeld met referenties:

```java
int[] numbers1 = {1, 2, 3};
int[] numbers2 = numbers1;
numbers2[0] = 99;
System.out.println(numbers1[0]); // 99
```

`numbers1` verandert ook, omdat beide variabelen naar hetzelfde array-object verwijzen.

# Strings

Een `String` is tekst in Java. Alles tussen dubbele aanhalingstekens is een string.

Voorbeelden:

```java
String firstName = "Stefan";
String message = "Hello, Java!";
```

Strings zijn referentietypes, maar Java maakt ze heel gemakkelijk in gebruik.

Nuttige string-bewerkingen:

```java
String name = "stefan";
System.out.println(name.length());      // 6
System.out.println(name.toUpperCase()); // STEFAN
System.out.println(name.startsWith("st")); // true
```

Strings zijn immutable (onveranderlijk). Dat betekent dat wanneer je een string "wijzigt", Java in werkelijkheid een nieuwe string maakt.

# Escape Sequences

Escape sequences laten je speciale tekens in strings plaatsen.

Ze beginnen met een backslash `\`.

Veelvoorkomende:

- `\"` - dubbel aanhalingsteken
- `\\` - backslash
- `\n` - nieuwe regel
- `\t` - tab

Voorbeeld:

```java
String text = "He said, \"Java is fun!\"\nNew line here.";
System.out.println(text);
```

Zonder escape sequences zouden bepaalde tekens je string-syntax breken.

# Arrays

Een array slaat meerdere waarden van hetzelfde type op in één variabele.

In plaats van veel variabelen zoals `score1`, `score2`, `score3`, gebruik je één array.

Voorbeeld:

```java
int[] scores = {90, 85, 100};
System.out.println(scores[0]); // 90
```

Arrayposities heten indexen, en indexering begint bij `0`, niet bij `1`.

Je kunt ook een lege array met vaste grootte maken:

```java
int[] numbers = new int[5]; // 5 plekken, standaardwaarde 0
```

# Multidimensionale Arrays

Een multidimensionale array is een array van arrays.

De meest voorkomende is een 2D-array, zoals een tabel met rijen en kolommen.

Voorbeeld:

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(matrix[1][2]); // 6
```

`matrix[1][2]` betekent: rij `1`, kolom `2`.

# Constanten

Een constante is een waarde die niet meer mag veranderen nadat je hem hebt ingesteld.

In Java gebruik je het sleutelwoord `final` voor constanten.

Voorbeeld:

```java
final double PI = 3.14159;
final int DAYS_IN_WEEK = 7;
```

Volgens conventie worden constanten meestal in hoofdletters met underscores geschreven.

Constanten maken je code veiliger en beter leesbaar.

# Rekenkundige Expressies

Rekenkundige expressies zijn wiskundige bewerkingen in code.

Java ondersteunt:

- `+` optellen
- `-` aftrekken
- `*` vermenigvuldigen
- `/` delen
- `%` rest (wat overblijft na deling)

Voorbeeld:

```java
int a = 10;
int b = 3;

System.out.println(a + b); // 13
System.out.println(a / b); // 3
System.out.println(a % b); // 1
```

Let op: `10 / 3` geeft `3`, omdat beide waarden integers zijn.

# Volgorde van Bewerkingen

Java volgt wiskundige prioriteitsregels bij het evalueren van expressies:

1. Haakjes `()`
2. Vermenigvuldigen/delen `* / %`
3. Optellen/aftrekken `+ -`

Voorbeeld:

```java
int result1 = 10 + 2 * 3;      // 16
int result2 = (10 + 2) * 3;    // 36
```

Gebruik haakjes wanneer je je bedoeling extra duidelijk wilt maken.

# Casting

Casting betekent het omzetten van een waarde van het ene type naar het andere.

Er zijn twee veelvoorkomende soorten:

- Impliciete casting (automatisch, veilig)
- Expliciete casting (handmatig)

Voorbeeld:

```java
int x = 10;
double y = x; // impliciete casting: int -> double
```

Expliciete casting:

```java
double price = 19.99;
int whole = (int) price; // 19
```

Wanneer je cast van een groter of preciezer type naar een kleiner type, kun je data verliezen.

# De Math-klasse

Java heeft een ingebouwde `Math`-klasse met handige wiskundige methodes.

Voorbeelden:

```java
System.out.println(Math.round(1.6));  // 2
System.out.println(Math.ceil(1.2));   // 2.0
System.out.println(Math.floor(1.8));  // 1.0
System.out.println(Math.max(10, 20)); // 20
System.out.println(Math.random());    // random getal 0.0 tot <1.0
```

Om een random integer binnen een bereik te krijgen, combineer je vaak `Math.random()` met casting.

# Getallen Formatteren

Soms wil je getallen netjes tonen aan gebruikers, zoals geldbedragen of percentages.

Java biedt formatter-klassen zoals `NumberFormat`.

Voorbeeld:

```java
import java.text.NumberFormat;

double amount = 1234.5;
String money = NumberFormat.getCurrencyInstance().format(amount);
System.out.println(money); // bv. €1.234,50 (afhankelijk van locale)
```

Je kunt ook als percentage formatteren:

```java
double ratio = 0.82;
String percent = NumberFormat.getPercentInstance().format(ratio);
System.out.println(percent); // 82%
```

Formatteren maakt output netter en professioneler.

# Invoer Lezen

Om invoer van de gebruiker in de console te lezen, gebruikt Java vaak de `Scanner`-klasse.

Voorbeeld:

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
System.out.print("What is your name? ");
String name = scanner.nextLine();

System.out.print("How old are you? ");
int age = scanner.nextInt();

System.out.println("Hello " + name + ", age " + age);
```

Hiermee kan je programma met gebruikers werken in plaats van alleen vaste waarden in code te gebruiken.

Tip: als je klaar bent met invoer, kun je de scanner sluiten met `scanner.close();`.

Hoe dit samenhangt:

- De sectie `Types` leert je wat data is en hoe je die opslaat.
- De volgende sectie (`Control Flow`) leert je hoe je programma beslissingen neemt met die data.

---

# Control Flow

## Vergelijkingsoperatoren

Vergelijkingsoperatoren vergelijken twee waarden. Het resultaat is altijd een `boolean` (`true` of `false`).

Zie deze operatoren als ja/nee-vragen die je programma stelt voordat het een pad kiest.

Veelgebruikte vergelijkingsoperatoren:

- `==` gelijk aan
- `!=` niet gelijk aan
- `>` groter dan
- `<` kleiner dan
- `>=` groter dan of gelijk aan
- `<=` kleiner dan of gelijk aan

```java
int age = 20;
System.out.println(age >= 18); // true
System.out.println(age == 21); // false
```

## Logische Operatoren

Logische operatoren laten je meerdere true/false-controles combineren.

- `&&` EN (beide voorwaarden moeten waar zijn)
- `||` OF (minstens één voorwaarde moet waar zijn)
- `!` NIET (keert true/false om)

```java
int age = 20;
boolean hasId = true;
System.out.println(age >= 18 && hasId); // true
```

## If-statements

Een `if`-statement voert code alleen uit als een voorwaarde waar is.

```java
int temperature = 30;

if (temperature > 25) {
    System.out.println("It's a warm day.");
}
```

Je kunt `else` toevoegen voor het andere geval:

```java
if (temperature > 25) {
    System.out.println("It's a warm day.");
} else {
    System.out.println("It's not warm.");
}
```

## If-statements Vereenvoudigen

Soms schrijven mensen lange `if`-statements om een boolean toe te wijzen. Dat kan eenvoudiger.

Lange versie:

```java
int income = 120_000;
boolean hasHighIncome;

if (income > 100_000)
    hasHighIncome = true;
else
    hasHighIncome = false;
```

Vereenvoudigde versie:

```java
boolean hasHighIncome = income > 100_000;
```

Schonere code is makkelijker te lezen en te onderhouden.

## De Ternary Operator

De ternary operator is een korte vorm van `if/else` om tussen twee waarden te kiezen.

Syntax:

```java
condition ? valueIfTrue : valueIfFalse
```

Voorbeeld:

```java
int income = 120_000;
String className = (income > 100_000) ? "First" : "Economy";
System.out.println(className);
```

Gebruik ternary voor eenvoudige keuzes, niet voor complexe logica.

## Switch-statements

`switch` is handig wanneer je één waarde vergelijkt met meerdere vaste opties.

```java
String role = "admin";

switch (role) {
    case "admin":
        System.out.println("You have full access.");
        break;
    case "moderator":
        System.out.println("You can manage comments.");
        break;
    default:
        System.out.println("You are a guest.");
}
```

`default` wordt uitgevoerd als geen enkele case matcht.

## Oefening - FizzBuzz

FizzBuzz is een klassieke oefening voor control flow.

Regels:

- Als een getal deelbaar is door zowel 3 als 5, print `FizzBuzz`
- Als het alleen deelbaar is door 3, print `Fizz`
- Als het alleen deelbaar is door 5, print `Buzz`
- Anders print je het getal

```java
int number = 15;

if (number % 3 == 0 && number % 5 == 0)
    System.out.println("FizzBuzz");
else if (number % 3 == 0)
    System.out.println("Fizz");
else if (number % 5 == 0)
    System.out.println("Buzz");
else
    System.out.println(number);
```

## For-loops

Een `for`-loop herhaalt code een bekend aantal keer.

Snelle onthoudtip:

- `for` = wanneer je ongeveer weet hoe vaak
- `while` = wanneer je doorgaat tot een voorwaarde verandert
- `do..while` = wanneer het minstens één keer moet draaien

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

Dit print de getallen 1 t/m 5.

## While-loops

Een `while`-loop herhaalt zolang de voorwaarde waar is.

```java
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}
```

Gebruik `while` wanneer je vooraf niet precies weet hoe vaak de loop moet draaien.

## Do..While-loops

Een `do..while`-loop voert het blok minstens één keer uit, en controleert daarna de voorwaarde.

```java
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

Dit is handig als de eerste uitvoering altijd moet gebeuren.

## Break en Continue

`break` stopt de loop meteen.  
`continue` slaat de huidige iteratie over en gaat door naar de volgende.

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3)
        continue; // skip 3
    if (i == 5)
        break;    // stop at 5
    System.out.println(i);
}
```

## For-Each Loop

Een for-each-loop is de makkelijkste manier om door arrays (of collecties) te lopen als je alleen de waarden nodig hebt.

```java
int[] numbers = {10, 20, 30};

for (int number : numbers) {
    System.out.println(number);
}
```

Gebruik for-each als je de indexpositie niet nodig hebt.

Korte samenvatting:

- vergelijkings/logische operatoren bepalen true/false-paden
- `if`/`switch` kiezen codevertakkingen
- loops herhalen code met verschillende controlestijlen

Hoe dit samenhangt:

- `Control Flow` leert hoe je programmagedrag stuurt.
- De volgende sectie (`Methods & Clean Code`) leert hoe je dat gedrag organiseert in schone, herbruikbare blokken.

---

# Methods & Clean Code

## Schone Code

Schone code is code die makkelijk te lezen, begrijpen en aanpassen is.

Zie methodes als gelabelde lades: elke lade heeft één doel, waardoor je logica snel kunt vinden en aanpassen.

Beginnerregel: schrijf code eerst voor mensen, daarna voor de computer.

Een paar gewoontes voor schone code:

- Gebruik duidelijke namen (`monthlyPayment` in plaats van `mp`)
- Houd methodes kort en gefocust
- Vermijd herhaling van dezelfde logica
- Houd opmaak consistent

```java
double monthlyPayment = 250.75;
System.out.println(monthlyPayment);
```

Kleine duidelijkheidsverbeteringen besparen later veel tijd.

Korte samenvatting:

- schone code is makkelijker te lezen, testen en aanpassen
- methodes verminderen duplicatie en verbeteren hergebruik
- refactoring houdt gedrag gelijk terwijl structuur verbetert

## Methodes Maken

Een methode is een benoemd codeblok dat één taak uitvoert.

In plaats van alles in `main` te schrijven, split je werk op in methodes.

```java
public static void greetUser(String name) {
    System.out.println("Hello " + name);
}
```

Aanroepen doe je zo:

```java
greetUser("Stefan");
```

Methodes maken je code herbruikbaar en makkelijker te testen.

## Refactoring

Refactoring betekent dat je de structuur van code verbetert zonder te veranderen wat het programma doet.

Je voegt geen features toe - je ruimt op en organiseert.

Voorbeeldidee:

- Voor: één lange methode met gemixte taken
- Na: meerdere kleine methodes met duidelijke namen

Refactor in kleine, veilige stappen en blijf je programma draaien.

## Methodes Extracten

Methodes extracten betekent dat je een codeblok verplaatst naar een eigen methode.

Voor:

```java
double principal = 100_000;
double annualInterest = 5;
int years = 30;

double monthlyInterest = annualInterest / 100 / 12;
int numberOfPayments = years * 12;
```

Na:

```java
double monthlyInterest = getMonthlyInterest(annualInterest);
int numberOfPayments = getNumberOfPayments(years);
```

Met helper-methodes:

```java
public static double getMonthlyInterest(double annualInterest) {
    return annualInterest / 100 / 12;
}

public static int getNumberOfPayments(int years) {
    return years * 12;
}
```

Dit maakt de hoofdflow makkelijker leesbaar.

## Herhalende Patronen Refactoren

Als je logica kopieert/plakt, is dat meestal een teken dat je een methode moet maken.

Voor (herhalend):

```java
System.out.print("Principal: ");
double principal = scanner.nextDouble();

System.out.print("Interest: ");
double interest = scanner.nextDouble();
```

Na (herbruikbare invoermethode):

```java
public static double readNumber(Scanner scanner, String prompt) {
    System.out.print(prompt);
    return scanner.nextDouble();
}
```

Dan:

```java
double principal = readNumber(scanner, "Principal: ");
double interest = readNumber(scanner, "Interest: ");
```

Minder herhaling betekent minder bugs en makkelijker onderhoud.

## Project - Betalingsschema

Doel: bouw een klein programma dat een leningsschema per maand toont.

Hoofdstappen:

1. Lees leninggegevens (hoofdsom, jaarlijkse rente, jaren)
2. Bereken vaste maandbetaling
3. Loop door elke maand
4. Toon resterend saldo na elke betaling

Dit is een sterk beginnersproject omdat het gebruikt maakt van:

- variabelen en types
- rekenkundige expressies
- methodes
- loops

## Oplossing

Een eenvoudige structuur kan er zo uitzien:

```java
public static void main(String[] args) {
    double principal = 100_000;
    double annualInterest = 5;
    int years = 30;

    double payment = calculateMonthlyPayment(principal, annualInterest, years);
    printPaymentSchedule(principal, annualInterest, years, payment);
}
```

Methode voor de maandbetalingsformule:

```java
public static double calculateMonthlyPayment(double principal, double annualInterest, int years) {
    double monthlyInterest = annualInterest / 100 / 12;
    int numberOfPayments = years * 12;
    return principal
            * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
            / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);
}
```

Methode voor het afdrukken van het schema:

```java
public static void printPaymentSchedule(double principal, double annualInterest, int years, double payment) {
    int months = years * 12;
    for (int month = 1; month <= months; month++) {
        double balance = calculateBalance(principal, annualInterest, years, month, payment);
        System.out.println("Month " + month + ": " + balance);
    }
}
```

## De Code Refactoren

Nadat het programma werkt, ruim je het op:

- Verplaats herhaalde wiskunde naar helper-methodes
- Gebruik constanten voor vaste getallen (`MONTHS_IN_YEAR`, `PERCENT`)
- Verbeter methodenamen
- Houd `main` kort en leesbaar

Voorbeeld van constanten:

```java
final byte MONTHS_IN_YEAR = 12;
final byte PERCENT = 100;
```

Eindmindset:

1. Laat het werken
2. Maak het duidelijk
3. Maak het schoon

Snelle gebruiksgids:

- extract methodes wanneer codeblokken zich herhalen
- houd methodes klein en doelgericht
- refactor telkens een beetje en test daarna opnieuw

Hoe dit samenhangt:

- `Methods & Clean Code` helpt je code structureren en verbeteren.
- De volgende sectie (`Debugging and Deploying Applications`) laat zien hoe je problemen oplost en je programma deelt.

---

# Debuggen en Applicaties Uitrollen

## Introductie

Code schrijven is maar één deel van programmeren. Je moet ook problemen oplossen en je app delen zodat anderen die kunnen uitvoeren.

Zie deze laatste sectie als "klaar voor de echte wereld": niet alleen code schrijven, maar ook onderhouden en opleveren.

Daar komen debuggen en uitrollen bij kijken:

- **Debugging** = problemen vinden en oplossen
- **Deploying/Packaging** = je app klaarmaken om buiten je IDE te draaien

## Soorten Fouten

In Java krijgen beginners meestal drie hoofdsoorten fouten:

1. **Syntax errors** - coderegels zijn gebroken (compiler vangt dit)
2. **Runtime errors** - programma crasht tijdens uitvoeren
3. **Logical errors** - programma draait, maar geeft verkeerde uitkomst

Voorbeeld:

```java
int result = 10 / 0; // runtime error: ArithmeticException
```

Als je het fouttype begrijpt, los je het sneller op.

Snelle gebruiksgids:

- syntax error -> los eerst grammatica/syntax op
- runtime error -> inspecteer de falende regel en invoer
- logical error -> controleer voorwaarden, formules en verwachtingen

## Veelvoorkomende Syntaxfouten

Syntaxfouten ontstaan wanneer Java-grammatica niet klopt.

Veelvoorkomende voorbeelden:

- Ontbrekende puntkomma `;`
- Fout gespelde keywords (`publc` in plaats van `public`)
- Ontbrekende accolades `{ }`
- Verkeerde quotes (`'Hello'` in plaats van `"Hello"` voor strings)

Voorbeeld met fouten:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello")
    }
}
```

Dit faalt door de ontbrekende puntkomma na `println`.

Fix:

```java
System.out.println("Hello");
```

## Java-applicaties Debuggen

Debuggen betekent dat je je programma stap voor stap onderzoekt om te vinden waar het misgaat.

Nuttige debugtools:

- Breakpoints
- Step Over / Step Into
- Variabele-inspectie
- Call stack-weergave

Eenvoudige manier om te debuggen:

1. Reproduceer de bug
2. Lees de foutmelding zorgvuldig
3. Controleer de regel in de stack trace
4. Zet breakpoints vóór de probleemregel
5. Volg variabelewaarden stap voor stap
6. Pas één ding tegelijk aan

Je kunt ook snelle print-debugging gebruiken:

```java
System.out.println("monthlyInterest = " + monthlyInterest);
System.out.println("numberOfPayments = " + numberOfPayments);
```

Dat helpt je te controleren of waarden zijn wat je verwacht.

### Mini Debug-checklist

- Crashte het programma? Lees eerst het exception-type.
- Draaide het programma maar gaf het verkeerde output? Controleer formules en voorwaarden opnieuw.
- Zijn je inputs geldig en binnen verwacht bereik?
- Heb je één ding aangepast en daarna opnieuw getest?

Debuggen is een vaardigheid die beter wordt met oefening.

Korte samenvatting:

- reproduceer het probleem consistent
- inspecteer data bij elke stap
- fix één variabele/factor tegelijk

## Java-applicaties Packagen

Packagen betekent dat je gecompileerde code bundelt zodat die via de command line kan draaien of gedeeld kan worden.

Een veelgebruikte package-vorm is een **JAR**-bestand.

Basisflow:

1. Compileer `.java`-bestanden naar `.class`-bestanden
2. Bundel ze in een `.jar`
3. Draai de jar met Java

Typische commando's:

```bash
javac Main.java
jar cfe app.jar Main Main.class
java -jar app.jar
```

Wat dit doet:

- `javac` compileert broncode
- `jar cfe` maakt een uitvoerbare JAR en zet de hoofdklasse
- `java -jar` start je packaged app

Voor grotere projecten automatiseren buildtools zoals Maven of Gradle dit proces.

Korte samenvatting:

- debuggen maakt code betrouwbaar
- packagen maakt code draaibaar buiten je IDE
- beide zijn kernonderdelen van echte softwareontwikkeling
