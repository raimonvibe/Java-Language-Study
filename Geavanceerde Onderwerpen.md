# Geavanceerde Onderwerpen

## Exceptions

### 1) Introductie

Exceptions zijn de manier waarop Java problemen meldt die optreden terwijl je programma draait.

In plaats van stil te crashen, geeft Java je een duidelijk foutobject dat je kunt afhandelen.

Zie een exception als een brandalarm in een gebouw:  
het zegt dat er iets misging en geeft je de kans om veilig te reageren.

Je kunt het ook zo zien: exceptions zijn Java's "probleemberichten" tussen code-onderdelen.  
Eén methode zegt: "Ik kon dit niet veilig afronden," en een andere methode beslist wat er daarna gebeurt.

### 2) Wat zijn Exceptions

Een exception is een object dat een fout beschrijft.

Voorbeeld: delen door nul.

```java
int result = 10 / 0; // ArithmeticException
```

Als je dit niet afhandelt, stopt het programma en wordt een foutmelding getoond.

Korte samenvatting:

- Exception = object dat een fout beschrijft
- Throwing = de fout melden
- Catching = de fout afhandelen

### 3) Soorten Exceptions

In eenvoudige termen heeft Java:

- **Checked exceptions** - moeten afgehandeld of gedeclareerd worden (bv. `IOException`)
- **Unchecked exceptions** - runtime-fouten (bv. `NullPointerException`)
- **Errors** - ernstige JVM-problemen (meestal niet afgevangen in applicatiecode)

Checked exceptions worden door de compiler gecontroleerd.

Onthoudtruc:

- Checked = "je moet nu iets met mij doen"
- Unchecked = "je mist een runtime-veiligheidscheck"
- Error = "het systeem zelf heeft een ernstig probleem"

### 4) Exception-hiërarchie

Alle exceptions komen voort uit `Throwable`.

Hoge-niveau structuur:

- `Throwable`
  - `Exception`
    - checked exceptions
    - `RuntimeException` (unchecked)
  - `Error`

Deze hiërarchie begrijpen helpt je exceptions op het juiste niveau af te vangen.

Waarom dit belangrijk is:

- Een brede catch (zoals `Exception`) is makkelijk, maar minder precies.
- Een specifieke catch (`IOException`, `ArithmeticException`) geeft duidelijkere afhandeling.

### 5) Exceptions Afvangen

Gebruik `try` en `catch` om fouten veilig af te handelen.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException ex) {
    System.out.println("Cannot divide by zero.");
}
```

Nu kan je programma verder draaien in plaats van direct te stoppen.

Zie `try/catch` als een veiligheidsnet:

- `try` = code die kan misgaan
- `catch` = back-upplan als dat gebeurt

### 6) Meerdere Exceptiontypes Afvangen

Je kunt verschillende exceptiontypes in aparte `catch`-blokken afvangen, of combineren.

```java
try {
    String text = null;
    System.out.println(text.length());
} catch (NullPointerException | ArithmeticException ex) {
    System.out.println("Invalid operation: " + ex.getMessage());
}
```

Dit houdt afhandeling compact wanneer de reactie hetzelfde is.

Gebruik één gecombineerde catch als de reactie hetzelfde is.  
Gebruik aparte catches als elk type een andere oplossing nodig heeft.

### 7) Het finally-blok

`finally` draait altijd, of er nu een exception gebeurt of niet.

Gebruik dit voor opruimwerk (bestanden sluiten, resources vrijgeven, enz.).

```java
try {
    System.out.println("Working...");
} catch (Exception ex) {
    System.out.println("Error.");
} finally {
    System.out.println("Always runs.");
}
```

Zie `finally` als: "ruim altijd je bureau op voordat je weggaat."

### 8) try-with-resources

Gebruik `try-with-resources` voor resources zoals bestanden/scanners.

Die worden dan automatisch gesloten.

```java
try (java.util.Scanner scanner = new java.util.Scanner(System.in)) {
    System.out.print("Name: ");
    String name = scanner.nextLine();
    System.out.println(name);
}
```

Dit is schoner en veiliger dan handmatig sluiten.

Waarom fijn voor beginners:

- Minder boilerplate
- Minder vergeten `close()`-aanroepen
- Veiligere cleanup standaard

### 9) Exceptions Gooien

Gebruik `throw` wanneer je zelf een fout wilt signaleren.

```java
public static void setAge(int age) {
    if (age < 0)
        throw new IllegalArgumentException("Age cannot be negative.");
}
```

Dit beschermt je methodes tegen ongeldige input.

Zie `throw` als een grens:
"Als deze input ongeldig is, stop ik hier en meld ik dat duidelijk."

### 10) Exceptions Opnieuw Gooien

Soms vang je een exception om te loggen of context toe te voegen, en gooi je hem daarna opnieuw.

```java
try {
    // risky code
} catch (Exception ex) {
    System.out.println("Logging error: " + ex.getMessage());
    throw ex;
}
```

Zo kan een hogere laag bepalen hoe de fout uiteindelijk afgehandeld wordt.

Veelvoorkomend patroon:

1. lage laag logt details
2. exception wordt opnieuw gegooid (of gewrapt)
3. hogere laag bepaalt gebruikersreactie

### 11) Custom Exceptions

Je kunt je eigen exceptionklasse maken voor domeinspecifieke problemen.

```java
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}
```

Custom exceptions maken fouten duidelijker en betekenisvoller.

Voorbeelden:

- `InvalidCouponCodeException`
- `InsufficientFundsException`
- `UserNotVerifiedException`

### 12) Chaining Exceptions

Exception chaining betekent dat je een exception inpakt in een andere, zodat de root cause behouden blijft.

```java
try {
    // low-level operation
} catch (Exception ex) {
    throw new RuntimeException("Failed to process payment.", ex);
}
```

Zo behoud je beide:

- business-context op hoger niveau
- technische oorzaak op lager niveau

### 13) Samenvatting

Belangrijkste punten:

- Exceptions helpen runtime-problemen veilig af te handelen
- Gebruik `try/catch/finally` voor controle en cleanup
- Gebruik bij voorkeur `try-with-resources` voor automatisch sluiten
- Gooi betekenisvolle exceptions bij ongeldige toestanden
- Gebruik custom en chained exceptions voor duidelijkere foutanalyse

Goede exception-afhandeling maakt je code veiliger, schoner en makkelijker te debuggen.

Korte samenvatting:

- `try/catch` = problemen afhandelen
- `finally` / try-with-resources = altijd opruimen
- `throw` = ongeldige toestand vroeg melden
- custom + chained exceptions = betere onderhoudbaarheid

Snelle gebruiksgids:

- gebruik `try/catch` als je lokaal kunt herstellen
- re-throw als een hogere laag moet beslissen
- gebruik custom exceptions voor business/domeinfouten

Hoe dit samenhangt:

- Exceptions gaan over veilig programmeren bij fouten.
- Generics (volgende sectie) gaan over veilig programmeren met types.
- Beide verminderen bugs vroeg in het proces.

---

## Generics

### 1) Introductie

Generics laten je klassen en methodes schrijven die veilig werken met verschillende datatypes.

Ze helpen je herhaling te vermijden en type-castingfouten te verminderen.

Zie generics als herbruikbare containers met labels:  
het label (`<T>`) vertelt Java wat erin mag.

### 2) Waarom Generics Nodig Zijn

Zonder generics slaan collecties vaak waarden op als `Object`, en moet je later casten.

Dat kan runtime-fouten veroorzaken.

Generics verplaatsen veel van die fouten naar compile-time, wat veiliger is.

Praktische analogie:

- Zonder generics = ongeëtiketteerde dozen
- Met generics = gelabelde dozen

Korte samenvatting:

- Generics vangen typefouten eerder
- Vroege fouten zijn goedkoper en makkelijker te herstellen

### 3) Een Slechte Oplossing

Een slechte aanpak is aparte klassen maken per type:

- `IntList`
- `StringList`
- `UserList`

Dat veroorzaakt duplicatie.  
Generics lossen dit op met één herbruikbare klasse.

Waarom dit slecht is:

- meer bestanden om te onderhouden
- dezelfde bug op meerdere plekken
- moeilijker schalen met nieuwe types

### 4) Generieke Klassen

Een generieke klasse gebruikt een typeparameter zoals `<T>`.

```java
class Box<T> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

Gebruik:

```java
Box<String> nameBox = new Box<>();
nameBox.setValue("Stefan");
```

Ook mogelijk:

```java
Box<Integer> ageBox = new Box<>();
ageBox.setValue(25);
```

### 5) Generics en Primitieve Types

Generics werken met referentietypes, niet met primitieve types.

Dus dit is ongeldig:

```java
// Box<int> box = new Box<>(); // invalid
```

Gebruik wrapper-klassen:

- `Integer` in plaats van `int`
- `Double` in plaats van `double`
- `Boolean` in plaats van `boolean`

Tip: Java autoboxing doet deze omzetting vaak automatisch.

### 6) Constraints

Je kunt generieke types beperken met bounds.

```java
class NumberBox<T extends Number> {
    private T value;
}
```

Nu moet `T` een `Number` zijn of een subclass daarvan (`Integer`, `Double`, ...).

Zie bounds als toegangsregels: alleen types die aan de regel voldoen mogen binnen.

### 7) Type Erasure

Java-generics worden geïmplementeerd met type erasure.

Op runtime worden veel generieke typedetails verwijderd.

Daarom kun je dingen zoals deze niet zomaar doen:

- `new T()`
- exacte runtime-checks op generic-type in simpele vorm

Mentaal model:

- compile-time: Java controleert typeveiligheid
- runtime: veel generic-detail is gewist

### 8) Comparable Interface

Generics werken vaak samen met `Comparable<T>` voor sorteren/vergelijken.

```java
class User implements Comparable<User> {
    private String name;

    public int compareTo(User other) {
        return this.name.compareTo(other.name);
    }
}
```

In de praktijk bepaalt `Comparable` de standaard sorteervolgorde van je klasse.

### 9) Generieke Methodes

Methodes kunnen ook generiek zijn, zelfs binnen niet-generieke klassen.

```java
public static <T> void printItem(T item) {
    System.out.println(item);
}
```

Aanroepen met verschillende types:

```java
printItem("Hello");
printItem(123);
```

### 10) Meerdere Typeparameters

Een klasse of methode kan meerdere typeparameters gebruiken.

```java
class Pair<K, V> {
    private K key;
    private V value;
}
```

Handig voor key-value-structuren.

### 11) Generics en Inheritance

Generieke types werken met inheritance, maar let op:

- `List<Dog>` is **geen** subtype van `List<Animal>`

Zelfs als `Dog` van `Animal` erft, zijn generieke containers standaard invariant.

Dit voorkomt onveilige toewijzingen.

### 12) Wildcards

Wildcards maken generieke API's flexibeler.

- `?` onbekend type
- `? extends T` upper bound (vooral lezen)
- `? super T` lower bound (vooral schrijven)

Voorbeeld:

```java
public static void printNames(java.util.List<? extends CharSequence> items) {
    for (CharSequence item : items)
        System.out.println(item);
}
```

Nu accepteert de methode `List<String>`, `List<StringBuilder>`, enz.

Onthoudregel:

- `? extends T` -> goed voor lezen
- `? super T` -> goed voor schrijven

### 13) Samenvatting

Kernpunten:

- Generics geven typeveiligheid en herbruikbaarheid
- Gebruik generieke klassen/methodes tegen duplicatie
- Gebruik bounds/wildcards voor flexibele maar veilige API's
- Gebruik wrappers voor primitieve types
- Begrijp de beperkingen van type erasure

Generics zijn een kernvaardigheid voor schone en schaalbare Java-code.

Korte samenvatting:

- generics = herbruikbare code + veilige types
- bounds/wildcards = flexibel maar gecontroleerd
- type erasure = waarom sommige runtime-dingen beperkt zijn

Snelle gebruiksgids:

- gebruik generics voor herbruikbare utilities/containers
- gebruik bounds als je bepaalde typecapaciteiten nodig hebt
- gebruik wildcards als je families van gerelateerde types wilt accepteren

Hoe dit samenhangt:

- Generics worden intensief gebruikt in collecties zoals `List<T>` en `Map<K, V>`.
- De volgende sectie (`Collections`) laat dat in dagelijkse Java-praktijk zien.

---

## Collections

### 1) Introductie

Collections helpen je groepen objecten op te slaan en te beheren in Java.

In plaats van voor elk scenario handmatig arrays te beheren, geeft het Collections Framework je herbruikbare datastructuren zoals lists, sets, queues en maps.

Zie collections als verschillende containers in het echte leven:

- `List` = geordend notitieblok
- `Set` = stickeralbum zonder dubbels
- `Queue` = wachtrij
- `Map` = woordenboek (sleutel -> betekenis)

### 2) Overzicht van het Collections Framework

Het Java Collections Framework is een set interfaces + klassen voor werken met gegroepeerde data.

Belangrijke onderdelen:

- Interfaces (`List`, `Set`, `Queue`, `Map`)
- Implementaties (`ArrayList`, `HashSet`, `PriorityQueue`, `HashMap`)
- Helpers (`Collections`-klasse)

Je programmeert meestal tegen interfaces en kiest daarna de beste implementatie.

Onthoud:

- Interface = contract ("wat het kan")
- Implementatie = motor ("hoe het werkt")

### 3) Waarom Iterables Nodig Zijn

Als je wilt dat custom objecten werken in loops zoals `for-each`, heeft Java een standaardmanier nodig om erdoorheen te lopen.

Daarom bestaat `Iterable`.

Zonder `Iterable` zou elke klasse zijn eigen loopstijl nodig hebben.

### 4) De Iterable Interface

`Iterable<T>` laat een object itereren in een `for-each`-loop.

Vereist één methode:

- `iterator()`

```java
class Numbers implements Iterable<Integer> {
    public java.util.Iterator<Integer> iterator() {
        return java.util.List.of(1, 2, 3).iterator();
    }
}
```

Dan kun je dit doen:

```java
for (int n : new Numbers())
    System.out.println(n);
```

### 5) De Iterator Interface

`Iterator<T>` gebruik je om element voor element door data te gaan.

Veelgebruikte methodes:

- `hasNext()`
- `next()`

```java
java.util.List<String> names = java.util.List.of("A", "B", "C");
java.util.Iterator<String> it = names.iterator();

while (it.hasNext())
    System.out.println(it.next());
```

Mentaal model:

- `hasNext()` vraagt: "Is er nog een item?"
- `next()` zegt: "Geef het volgende item."

### 6) De Collection Interface

`Collection<E>` is een root-interface voor veel collectietypes (`List`, `Set`, `Queue`).

Veelgebruikte operaties:

- `add()`
- `remove()`
- `contains()`
- `size()`
- `isEmpty()`

```java
java.util.Collection<String> items = new java.util.ArrayList<>();
items.add("Java");
items.add("Spring");
System.out.println(items.size()); // 2
```

### 7) De List Interface

`List<E>` is een geordende collectie die duplicaten toelaat.

Voorbeelden: `ArrayList`, `LinkedList`

```java
java.util.List<String> courses = new java.util.ArrayList<>();
courses.add("Java");
courses.add("Java");
courses.add("SQL");
System.out.println(courses.get(0)); // Java
```

Gebruik `List` wanneer volgorde belangrijk is of duplicaten toegestaan zijn.

### 8) De Comparable Interface

`Comparable<T>` definieert natuurlijke sortering binnen een klasse.

```java
class User implements Comparable<User> {
    String name;

    public int compareTo(User other) {
        return this.name.compareTo(other.name);
    }
}
```

Java weet zo standaard hoe `User`-objecten gesorteerd moeten worden.

### 9) De Comparator Interface

`Comparator<T>` definieert externe/custom sorteerregels.

```java
java.util.Comparator<String> byLength =
        (a, b) -> Integer.compare(a.length(), b.length());
```

Gebruik `Comparator` wanneer je meerdere sorteerstijlen wilt zonder klassecode aan te passen.

### 10) De Queue Interface

`Queue<E>` is ontworpen voor verwerking in volgorde, vaak FIFO (first in, first out).

Veelgebruikte methodes:

- `offer()` toevoegen
- `poll()` head verwijderen
- `peek()` head bekijken

```java
java.util.Queue<String> queue = new java.util.ArrayDeque<>();
queue.offer("task1");
queue.offer("task2");
System.out.println(queue.poll()); // task1
```

### 11) De Set Interface

`Set<E>` bewaart unieke waarden (geen duplicaten).

Voorbeelden: `HashSet`, `LinkedHashSet`, `TreeSet`

```java
java.util.Set<String> tags = new java.util.HashSet<>();
tags.add("java");
tags.add("java");
System.out.println(tags.size()); // 1
```

Gebruik `Set` wanneer uniekheid belangrijk is.

### 12) Hash Tables

Hash-gebaseerde collecties (`HashSet`, `HashMap`) gebruiken hashing voor snelle lookup.

Gemiddelde performance voor add/find/remove is ongeveer O(1).

Voor custom objecten in hash-collecties moet je correct overriden:

- `equals()`
- `hashCode()`

Deze twee moeten consistent zijn.

### 13) De Map Interface

`Map<K, V>` slaat key-value-paren op.

Keys zijn uniek, values mogen herhalen.

```java
java.util.Map<String, Integer> scores = new java.util.HashMap<>();
scores.put("Stefan", 95);
scores.put("Alex", 88);
System.out.println(scores.get("Stefan")); // 95
```

Nuttige methodes:

- `put()`
- `get()`
- `containsKey()`
- `remove()`

### 14) Samenvatting

Belangrijkste punten:

- Gebruik `List` voor geordende data met duplicaten
- Gebruik `Set` voor unieke data
- Gebruik `Queue` voor verwerkingsflow
- Gebruik `Map` voor key-value-opzoeking
- Gebruik `Comparable`/`Comparator` voor sorteren

De juiste collectie kiezen maakt je code simpeler en efficiënter.

Korte samenvatting:

- `List` = geordend + duplicaten toegestaan
- `Set` = alleen unieke waarden
- `Queue` = verwerkingsvolgorde
- `Map` = key -> value lookup

Hoe dit samenhangt:

- Collections beantwoorden "waar data wordt opgeslagen."
- Lambda's en functionele interfaces (volgende) beantwoorden "hoe gedrag wordt doorgegeven."
- Streams combineren later beide.

---

## Lambda-expressies en Functionele Interfaces

### 1) Introductie

Lambda's laten je kortere, duidelijkere code schrijven voor gedrag dat je wilt doorgeven.

Ze worden veel gebruikt met collections, streams en moderne Java-API's.

Zie een lambda als een mini-functie die je als data kunt doorgeven.

Korte samenvatting:

- functionele interface = vorm/contract van gedrag
- lambda = snelle implementatie van dat gedrag

### 2) Functionele Interfaces

Een functionele interface heeft precies één abstracte methode.

```java
@FunctionalInterface
interface Printer {
    void print(String message);
}
```

Deze interface kun je implementeren met een lambda.

### 3) Anonieme Inner Classes

Vóór lambda's gebruikte Java vaak anonieme classes voor kort gedrag.

```java
Printer p = new Printer() {
    public void print(String message) {
        System.out.println(message);
    }
};
```

Dit werkt, maar is vrij uitgebreid.

### 4) Lambda-expressies

Een lambda is een kortere manier om een functionele interface te implementeren.

```java
Printer p = message -> System.out.println(message);
p.print("Hello");
```

Zelfde gedrag, minder boilerplate.

### 5) Variable Capture

Lambda's kunnen lokale variabelen uit de omgeving gebruiken, maar die variabelen moeten final of effectief final zijn.

```java
String prefix = "Log: ";
Printer p = msg -> System.out.println(prefix + msg);
```

Als je `prefix` daarna opnieuw toewijst, wijst Java dit af.

### 6) Method References

Method references zijn snelkoppelingen wanneer een lambda slechts één methode aanroept.

```java
Printer p = System.out::println;
p.print("Hello");
```

Ze verbeteren leesbaarheid in veel gevallen.

### 7) Ingebouwde Functionele Interfaces

Java biedt veelgebruikte functionele interfaces in `java.util.function`, zoals:

- `Consumer<T>`
- `Supplier<T>`
- `Function<T, R>`
- `Predicate<T>`
- `BinaryOperator<T>`
- `UnaryOperator<T>`

Gebruik deze bij voorkeur in plaats van telkens nieuwe interfaces te maken.

### 8) De Consumer Interface

`Consumer<T>` neemt een waarde en geeft niets terug.

```java
java.util.function.Consumer<String> print = s -> System.out.println(s);
print.accept("Java");
```

Handig voor side effects zoals loggen of printen.

### 9) Consumer Chainen

Je kunt consumers koppelen met `andThen`.

```java
java.util.function.Consumer<String> c1 = s -> System.out.println("First: " + s);
java.util.function.Consumer<String> c2 = s -> System.out.println("Second: " + s);

c1.andThen(c2).accept("Item");
```

Beide draaien in volgorde.

### 10) De Supplier Interface

`Supplier<T>` levert een waarde en heeft geen input.

```java
java.util.function.Supplier<Double> random = () -> Math.random();
System.out.println(random.get());
```

Handig voor lazy value creation.

### 11) De Function Interface

`Function<T, R>` transformeert één waarde naar een andere.

```java
java.util.function.Function<String, Integer> length = s -> s.length();
System.out.println(length.apply("Java")); // 4
```

Perfect voor mapping/conversies.

### 12) Functions Combineren

Functions kun je combineren met `andThen` en `compose`.

```java
java.util.function.Function<Integer, Integer> times2 = x -> x * 2;
java.util.function.Function<Integer, Integer> plus1 = x -> x + 1;

System.out.println(times2.andThen(plus1).apply(3)); // 7
```

Dit helpt je herbruikbare verwerkingspipelines te bouwen.

### 13) De Predicate Interface

`Predicate<T>` controleert een voorwaarde en geeft boolean terug.

```java
java.util.function.Predicate<String> isLong = s -> s.length() > 5;
System.out.println(isLong.test("Stefan")); // true
```

Handig om data te filteren.

### 14) Predicates Combineren

Combineer predicates met `and`, `or` en `negate`.

```java
java.util.function.Predicate<String> startsWithA = s -> s.startsWith("A");
java.util.function.Predicate<String> longName = s -> s.length() > 3;

System.out.println(startsWithA.and(longName).test("Alex")); // true
```

Zo hou je voorwaarden modulair en leesbaar.

### 15) De BinaryOperator Interface

`BinaryOperator<T>` neemt twee waarden van hetzelfde type en geeft één waarde van hetzelfde type terug.

```java
java.util.function.BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(2, 3)); // 5
```

Nuttig voor combineren of reduceren.

### 16) De UnaryOperator Interface

`UnaryOperator<T>` neemt één waarde en geeft hetzelfde type terug.

```java
java.util.function.UnaryOperator<Integer> square = x -> x * x;
System.out.println(square.apply(4)); // 16
```

Nuttig voor same-type transformaties.

### 17) Samenvatting

Belangrijkste punten:

- Lambda's maken functionele code compacter
- Functionele interfaces definiëren één gedragscontract
- Ingebouwde interfaces dekken de meeste gevallen
- Compositie/chaining bouwt herbruikbare logica

Korte samenvatting:

- lambda's maken gedrag makkelijk doorgeefbaar
- functionele interfaces standaardiseren gedragspatronen
- compositie helpt grotere logica opbouwen uit kleine blokken

Hoe dit samenhangt:

- Functionele interfaces definiëren contracten voor gedrag.
- Lambda's vullen die contracten snel in.
- Streams (volgende sectie) gebruiken dit overal (`map`, `filter`, `reduce`).

---

## Streams

### 1) Introductie

Streams laten je collectiedata verwerken in een duidelijke pipeline-stijl.

Je kunt bewerkingen chainen zoals filteren, mappen, sorteren en collecteren.

Zie een stream-pipeline als een productielijn:

- `filter` haalt ongewenste items weg
- `map` transformeert items
- `collect` verpakt het eindresultaat

### 2) Imperatief vs Functioneel Programmeren

Imperatieve stijl zegt **hoe** je stappen uitvoert.  
Functionele stijl zegt **welk resultaat** je wilt.

Imperatief:

```java
java.util.List<String> result = new java.util.ArrayList<>();
for (String name : java.util.List.of("alex", "bob"))
    result.add(name.toUpperCase());
```

Functioneel (stream):

```java
java.util.List<String> result = java.util.List.of("alex", "bob")
        .stream()
        .map(String::toUpperCase)
        .toList();
```

### 3) Een Stream Maken

Je kunt streams maken uit:

- collecties: `list.stream()`
- arrays: `Arrays.stream(array)`
- losse waarden: `Stream.of(...)`
- ranges: `IntStream.range(...)`

```java
java.util.stream.Stream<String> stream = java.util.stream.Stream.of("A", "B", "C");
```

Tip: streams zijn single-use; na een terminal operation maak je een nieuwe stream.

### 4) Elementen Mappen

`map()` transformeert elk element naar iets anders.

```java
java.util.List<Integer> lengths = java.util.List.of("Java", "Stream")
        .stream()
        .map(String::length)
        .toList();
```

### 5) Elementen Filteren

`filter()` houdt alleen elementen die aan een voorwaarde voldoen.

```java
java.util.List<String> longNames = java.util.List.of("Al", "Alex", "Sam")
        .stream()
        .filter(name -> name.length() > 3)
        .toList();
```

### 6) Streams Slicen

Gebruik:

- `limit(n)` voor de eerste `n` items
- `skip(n)` om de eerste `n` over te slaan
- `takeWhile(...)` / `dropWhile(...)` (geordende streams)

```java
java.util.List<Integer> sliced = java.util.List.of(1, 2, 3, 4, 5)
        .stream()
        .skip(1)
        .limit(3)
        .toList(); // [2, 3, 4]
```

### 7) Streams Sorteren

Gebruik `sorted()` voor natuurlijke volgorde, of geef een comparator mee voor custom volgorde.

```java
java.util.List<String> sorted = java.util.List.of("Bob", "Alex", "Chris")
        .stream()
        .sorted()
        .toList();
```

Custom:

```java
java.util.List<String> byLength = java.util.List.of("Bob", "Alexander", "Chris")
        .stream()
        .sorted(java.util.Comparator.comparingInt(String::length))
        .toList();
```

### 8) Unieke Elementen

Gebruik `distinct()` om duplicaten te verwijderen.

```java
java.util.List<Integer> unique = java.util.List.of(1, 2, 2, 3, 3, 3)
        .stream()
        .distinct()
        .toList(); // [1, 2, 3]
```

### 9) Elementen Peeken

`peek()` is handig als debug-checkpoint in stream-pipelines.

```java
java.util.List.of("a", "b", "c")
        .stream()
        .peek(x -> System.out.println("Before: " + x))
        .map(String::toUpperCase)
        .peek(x -> System.out.println("After: " + x))
        .toList();
```

Gebruik `peek()` niet voor belangrijke business side effects.

### 10) Simpele Reducers

Reducers berekenen één waarde uit streamdata:

- `count()`
- `anyMatch()`, `allMatch()`, `noneMatch()`
- `findFirst()`, `findAny()`

```java
long count = java.util.List.of("A", "B", "C").stream().count();
```

### 11) Een Stream Reducen

Gebruik `reduce()` om elementen tot één resultaat te combineren.

```java
int sum = java.util.List.of(1, 2, 3, 4)
        .stream()
        .reduce(0, Integer::sum);
```

### 12) Collectors

Collectors zetten streamresultaten om naar containers of samenvattingen.

```java
java.util.List<String> list = java.util.List.of("a", "b")
        .stream()
        .map(String::toUpperCase)
        .collect(java.util.stream.Collectors.toList());
```

Veelgebruikte collectors:

- `toList()`
- `toSet()`
- `toMap()`
- `joining()`
- `counting()`

### 13) Elementen Groeperen

`groupingBy()` groepeert elementen op een key.

```java
java.util.Map<Integer, java.util.List<String>> grouped = java.util.List.of("a", "bb", "cc", "ddd")
        .stream()
        .collect(java.util.stream.Collectors.groupingBy(String::length));
```

### 14) Elementen Partitioneren

`partitioningBy()` splitst elementen in twee groepen (`true` / `false`) op basis van een predicate.

```java
java.util.Map<Boolean, java.util.List<Integer>> partitioned = java.util.List.of(1, 2, 3, 4)
        .stream()
        .collect(java.util.stream.Collectors.partitioningBy(n -> n % 2 == 0));
```

### 15) Primitive Type Streams

Java heeft gespecialiseerde streams voor primitieve types:

- `IntStream`
- `LongStream`
- `DoubleStream`

```java
int total = java.util.stream.IntStream.rangeClosed(1, 5).sum(); // 15
```

### 16) Samenvatting

Streams helpen je data verwerken met leesbare, chainbare operaties.

Belangrijk:

- maak pipelines met map/filter/sort
- gebruik reducers/collectors voor eindresultaten
- gebruik grouping/partitioning voor gestructureerde output
- gebruik primitive streams bij veel numerieke verwerking

Korte samenvatting:

- `map` transformeert
- `filter` selecteert
- `reduce` combineert
- `collect` verpakt het resultaat

Hoe dit samenhangt:

- Streams bouwen voort op collections + lambda's.
- Concurrency (volgende) focust op veilig parallel uitvoeren.
- Daarna maakt Executor Framework dit praktisch op hoog niveau.

---

## Concurrency en Multi-threading

### 1) Introductie

Concurrency betekent meerdere taken tegelijk afhandelen.

In Java gebeurt dit vaak met threads zodat programma's responsiever zijn en CPU-resources beter gebruiken.

Zie threads als meerdere koks in één keuken.

Korte samenvatting:

- concurrency = meerdere taken tegelijk afhandelen
- thread = één uitvoerpad
- grootste uitdaging = gedeelde data veilig houden

### 2) Processen en Threads

- Een **proces** is een draaiend programma met eigen geheugenruimte.
- Een **thread** is een kleinere execution unit binnen een proces.

Eén proces kan meerdere threads hebben die geheugen delen.

### 3) Een Thread Starten

Je start een nieuwe thread door code (`Runnable`) aan `Thread` te geven.

```java
Thread thread = new Thread(() -> System.out.println("Running in thread"));
thread.start();
```

Gebruik `start()`, niet `run()`, om echt een aparte thread te krijgen.

### 4) Een Thread Pauzeren

Gebruik `Thread.sleep(milliseconds)` om de huidige thread te pauzeren.

```java
try {
    Thread.sleep(1000);
} catch (InterruptedException e) {
    Thread.currentThread().interrupt();
}
```

### 5) Een Thread Joinen

`join()` laat één thread wachten tot een andere klaar is.

```java
Thread worker = new Thread(() -> System.out.println("Work done"));
worker.start();
worker.join(); // wait for worker
```

### 6) Een Thread Onderbreken

Interrupten vraagt een thread om te stoppen waar hij mee bezig is.

```java
thread.interrupt();
```

Zie interrupt als een nette stopvraag, niet als force-kill.

### 7) Concurrency-problemen

Meerdere threads die mutable data delen kunnen bugs veroorzaken zoals:

- verloren updates
- inconsistente reads
- onverwachte volgorde

Deze bugs zijn vaak moeilijk reproduceerbaar.

### 8) Race Conditions

Een race condition ontstaat als resultaat afhangt van thread-timing.

Voorbeeld: twee threads verhogen dezelfde teller tegelijk en één update gaat verloren.

```java
counter++; // not atomic
```

### 9) Strategieën voor Thread Safety

Veelgebruikte strategieën:

- vermijd gedeelde mutable state
- gebruik immutable objecten
- gebruik synchronization/locks
- gebruik thread-safe collecties/atomic classes

Kies de simpelste strategie die het probleem oplost.

### 10) Confinement

Confinement betekent data beperken tot één thread.

Als slechts één thread data kan bereiken, is synchronisatie voor die data niet nodig.

Voorbeeld: lokale variabelen in een methode zijn thread-confined.

### 11) Locks

Locks zorgen dat maar één thread tegelijk kritieke code uitvoert.

```java
java.util.concurrent.locks.Lock lock = new java.util.concurrent.locks.ReentrantLock();
lock.lock();
try {
    // critical section
} finally {
    lock.unlock();
}
```

Altijd unlocken in `finally`.

### 12) Het synchronized-keyword

`synchronized` is ingebouwde Java-locking.

```java
public synchronized void increment() {
    count++;
}
```

### 13) Het volatile-keyword

`volatile` zorgt ervoor dat wijzigingen aan een variabele snel zichtbaar zijn voor andere threads.

```java
private volatile boolean running = true;
```

Gebruik dit voor zichtbaarheid, niet voor compound atomics zoals `count++`.

### 14) Thread Signalling met wait() en notify()

Threads kunnen coördineren via wachten en notificeren op hetzelfde monitorobject.

```java
synchronized (lock) {
    lock.wait();   // releases lock and waits
    lock.notify(); // wakes one waiting thread
}
```

### 15) Atomic Objects

Atomic classes voeren thread-safe operaties uit zonder handmatige locks.

```java
java.util.concurrent.atomic.AtomicInteger counter = new java.util.concurrent.atomic.AtomicInteger();
counter.incrementAndGet();
```

### 16) Adders

`LongAdder` / `DoubleAdder` zijn geoptimaliseerd voor high-contention counters.

```java
java.util.concurrent.atomic.LongAdder adder = new java.util.concurrent.atomic.LongAdder();
adder.increment();
long total = adder.sum();
```

### 17) Synchronized Collections

Java biedt synchronized wrappers:

```java
java.util.List<String> list = java.util.Collections.synchronizedList(new java.util.ArrayList<>());
```

### 18) Concurrent Collections

`java.util.concurrent` bevat collecties voor concurrency, zoals:

- `ConcurrentHashMap`
- `CopyOnWriteArrayList`
- `ConcurrentLinkedQueue`

### 19) Samenvatting

Kernpunten:

- threads verbeteren responsiviteit en throughput
- gedeelde mutable state veroorzaakt meeste concurrencybugs
- gebruik synchronization, locks, atomics en concurrent collections bewust
- eerst correctheid, daarna optimalisatie

Korte samenvatting:

- begin met veilige gedeelde-state logica
- optimaliseer performance pas daarna
- foutieve concurrencylogica debuggen is lastig

Hoe dit samenhangt:

- Deze sectie legt thread-safety fundamenten uit.
- De volgende sectie (`Executor Framework`) geeft hogere-level tools zodat je niet alles handmatig beheert.

---

## Het Executor Framework

### 1) Introductie

Het Executor Framework helpt je threads schoner en veiliger beheren dan wanneer je alles met de hand doet.

Zie het als een taakmanager: jij levert jobs aan, het framework kiest welke worker-thread ze uitvoert.

Korte samenvatting:

- jij focust op taken
- framework focust op threadbeheer

### 2) Thread Pools

Een thread pool is een groep herbruikbare worker-threads.

In plaats van per taak een nieuwe thread te maken, submit je taken aan de pool.

Voordelen:

- betere performance
- minder overhead door thread-creatie
- gecontroleerd resourcegebruik

### 3) Executors

De `Executors` utility-klasse maakt veelvoorkomende executortypes.

```java
java.util.concurrent.ExecutorService executor =
        java.util.concurrent.Executors.newFixedThreadPool(4);

executor.submit(() -> System.out.println("Task running"));
executor.shutdown();
```

Veelgebruikte factories:

- `newFixedThreadPool(n)`
- `newCachedThreadPool()`
- `newSingleThreadExecutor()`

Snelle keuzegids:

- fixed pool -> stabiele, voorspelbare concurrency
- cached pool -> korte, bursty taken
- single-thread executor -> taken strikt één voor één

### 4) Callables en Futures

`Runnable` geeft geen waarde terug.  
`Callable<T>` kan wel een waarde teruggeven (en exceptions gooien).

```java
java.util.concurrent.Future<Integer> future = executor.submit(() -> 1 + 2);
int result = future.get(); // blocks until done
```

`Future` vertegenwoordigt een resultaat dat later beschikbaar komt.

Analogie: afhaaleten bestellen

- `Callable` = de kok die eten maakt en teruggeeft
- `Future` = je afhaalbon

Je krijgt de bon meteen, maar het eten kan nog in de keuken zijn.

```java
java.util.concurrent.Callable<Integer> task = () -> {
    // do some work...
    return 42;
};

java.util.concurrent.Future<Integer> future = executor.submit(task);

// later...
Integer result = future.get(); // waits until ready
```

### 5) Asynchroon Programmeren

Asynchroon programmeren betekent taken starten zonder de huidige thread direct te blokkeren.

Dit verhoogt responsiviteit, vooral bij I/O en externe calls.

### 6) CompletableFuture

`CompletableFuture` is een krachtige API voor async workflows.

Ondersteunt:

- callbacks bij afronding
- transformaties
- compositie/combinatie
- exception-handling

### 7) Een CompletableFuture Maken

Maak er één met `supplyAsync` of `runAsync`.

```java
java.util.concurrent.CompletableFuture<Integer> future =
        java.util.concurrent.CompletableFuture.supplyAsync(() -> 42);
```

### 8) Een Asynchrone API Implementeren

In plaats van een directe waarde terug te geven, geef je `CompletableFuture<T>` terug.

```java
public java.util.concurrent.CompletableFuture<String> getUserNameAsync() {
    return java.util.concurrent.CompletableFuture.supplyAsync(() -> "Stefan");
}
```

### 9) Code Draaien bij Voltooiing

Gebruik completion-methodes:

- `thenRun()`
- `thenAccept()`
- `thenApply()`

```java
future.thenAccept(value -> System.out.println("Done: " + value));
```

### 10) Exceptions Afhandelen

Gebruik `exceptionally`, `handle` of `whenComplete`.

```java
future.exceptionally(ex -> {
    System.out.println("Error: " + ex.getMessage());
    return -1;
});
```

### 11) Een CompletableFuture Transformeren

Gebruik `thenApply` om resultaatwaarde te transformeren.

```java
java.util.concurrent.CompletableFuture<String> nameFuture =
        java.util.concurrent.CompletableFuture.supplyAsync(() -> "stefan")
                .thenApply(String::toUpperCase);
```

### 12) CompletableFutures Componeren

Gebruik `thenCompose` wanneer de tweede async taak afhangt van het eerste resultaat.

```java
java.util.concurrent.CompletableFuture<String> composed =
        getUserNameAsync().thenCompose(name -> getGreetingAsync(name));
```

### 13) CompletableFutures Combineren

Gebruik `thenCombine` wanneer twee onafhankelijke futures beide nodig zijn.

```java
futureA.thenCombine(futureB, (a, b) -> a + " " + b);
```

### 14) Wachten op Veel Taken

Gebruik `CompletableFuture.allOf(...)`.

```java
java.util.concurrent.CompletableFuture<Void> all =
        java.util.concurrent.CompletableFuture.allOf(future1, future2, future3);
all.join();
```

### 15) Wachten op de Eerste Taak

Gebruik `CompletableFuture.anyOf(...)` om door te gaan met de eerste afgeronde taak.

```java
java.util.concurrent.CompletableFuture<Object> first =
        java.util.concurrent.CompletableFuture.anyOf(future1, future2);
```

### 16) Timeouts Afhandelen

Je kunt wachttijd limiteren op futures.

```java
future.orTimeout(2, java.util.concurrent.TimeUnit.SECONDS);
```

Of fallback geven:

```java
future.completeOnTimeout("default", 2, java.util.concurrent.TimeUnit.SECONDS);
```

### 17) Project - Best Price Finder

Projectidee: haal prijsquotes op van meerdere winkels en toon de beste prijs.

Waarom dit project goed is:

- meerdere onafhankelijke taken
- async calls
- resultaten combineren
- timeout/error-handling

### 18) Oplossing - Eén Quote Ophalen

Elke store-call kan `CompletableFuture<Quote>` teruggeven.

```java
public java.util.concurrent.CompletableFuture<Double> getQuoteAsync(String store) {
    return java.util.concurrent.CompletableFuture.supplyAsync(() -> fetchPrice(store));
}
```

### 19) Oplossing - Meerdere Quotes Ophalen

Roep veel stores tegelijk aan en wacht dan op allemaal.

```java
java.util.List<java.util.concurrent.CompletableFuture<Double>> futures = stores.stream()
        .map(this::getQuoteAsync)
        .toList();

java.util.concurrent.CompletableFuture.allOf(futures.toArray(new java.util.concurrent.CompletableFuture[0])).join();
```

Verzamel daarna resultaten en kies de minimumprijs.

### 20) Oplossing - Willekeurige Vertragingen

Echte API's reageren met verschillende snelheden. Willekeurige vertragingen simuleren helpt timeoutgedrag realistisch te testen.

Voorbeeld:

- voeg random sleep toe in mock `fetchPrice`
- test welke store als eerste terugkomt
- verifieer fallback bij te trage store

Korte samenvatting:

- gebruik executors voor gecontroleerde threaduitvoering
- gebruik futures voor latere resultaten
- gebruik `CompletableFuture` voor chained async workflows
- gebruik timeouts/fallbacks voor betrouwbaarheid
