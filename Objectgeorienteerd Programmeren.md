# Objectgeorienteerd Programmeren

## Aan de slag

### 1) Introductie

Object-oriented Programming (OOP) is een manier van programmeren waarbij je code organiseert rond **objecten**.

Zie OOP als bouwen met Lego-blokken: elk object is een blok met eigen data en gedrag.

Een object is als een echt ding in je programma.  
In een schoolapp kun je bijvoorbeeld objecten hebben zoals:

- `Student`
- `Course`
- `Teacher`

Elk object kan hebben:

- **Data** (velden/properties), zoals de naam van een student
- **Gedrag** (methodes), zoals `enroll()` of `printReport()`

OOP helpt je om echte problemen op een natuurlijke manier te modelleren.

Korte samenvatting:

- Object = ding met data + gedrag
- Class = blauwdruk om die dingen te maken
- OOP = code organiseren rond die dingen

### 2) Programmeerparadigma's

Een programmeerparadigma is een stijl of aanpak om code te schrijven.

Veelvoorkomende paradigma's:

- **Procedureel programmeren** - code is georganiseerd als stappen en functies
- **Object-oriented programming** - code is georganiseerd als objecten en klassen
- **Functioneel programmeren** - code is georganiseerd rond pure functies en immutability

Java ondersteunt meerdere stijlen, maar OOP is een van de sterkste kanten van Java.

Eenvoudige vergelijking:

Procedurele stijl vraagt vaak:  
"Welke stappen moeten gebeuren?"

OOP-stijl vraagt vaak:  
"Welke objecten heb ik, en wat moet elk object doen?"

Beide kunnen problemen oplossen, maar OOP is vooral handig bij grotere applicaties.

Snelle gebruiksgids:

- Procedurele stijl is vaak prima voor heel kleine scripts.
- OOP-stijl is meestal beter als je project veel gerelateerde entiteiten en regels heeft.

### 3) Voordelen van Object-oriented Programming

OOP geeft structuur, vooral wanneer projecten groter worden.

Belangrijkste beginnersvriendelijke voordelen:

- **Betere organisatie** - gerelateerde data en gedrag blijven samen in één klasse
- **Herbruikbaarheid** - je kunt klassen op meerdere plekken hergebruiken
- **Makkelijker onderhoud** - met een duidelijke structuur vind je bugs sneller
- **Schaalbaarheid** - makkelijker nieuwe features toevoegen zonder oude code te breken

Snel voorbeeld:

Als je één keer een `Car`-klasse maakt, kun je daar veel car-objecten van maken:

```java
Car car1 = new Car();
Car car2 = new Car();
```

Je schrijft de klasse één keer, en hergebruikt die daarna vaak.

Zie klassen als sjablonen en objecten als kopieën van dat sjabloon.

Snelle gebruiksgids:

- Gebruik klassen wanneer je echte entiteiten wilt modelleren (user, order, product, course).
- Zet gerelateerde data en acties in dezelfde klasse voor duidelijkheid.

Korte samenvatting:

- OOP verbetert structuur wanneer projecten groeien
- Hergebruik ontstaat doordat je meerdere objecten uit één klasse maakt
- Betere structuur betekent meestal makkelijker onderhoud en opschaling

Hoe dit samenhangt:

- `Aan de slag` legt de OOP-mindset uit.
- Daarna toont `Kernconcepten van OOP` de praktische tools die je dagelijks gebruikt.

---

## Kernconcepten van OOP

### 1) Introductie

Nu gaan we dieper in op de bouwstenen van OOP in Java.

Zie deze sectie als het praktische deel: hoe je klassen maakt, objecten maakt en schonere code ontwerpt.

Korte samenvatting:

- klassen definiëren structuur
- objecten bevatten echte data
- kern-OOP-tools helpen je code veilig, herbruikbaar en wijzigbaar te houden

Overeenkomst tussen kernconcepten:

- Encapsulatie beschermt data.
- Abstractie verbergt complexiteit.
- Lage coupling houdt onderdelen flexibel.

Samen zorgen ze voor code die zowel veilig als onderhoudbaar is.

### 2) Klassen en Objecten

Een **class** is een blauwdruk.  
Een **object** is een echte instantie gemaakt op basis van die blauwdruk.

Voorbeeld:

- Class: `Car`
- Object: `myCar`

```java
class Car {
    String brand;
}
```

`Car` definieert wat een car-object kan bevatten.

Snelle onthoudregel:

- Class = plan
- Object = echt ding gebouwd vanuit dat plan

### 3) Klassen maken

Wanneer je een klasse maakt, begin je met:

- Velden (data)
- Methodes (gedrag)

```java
class Employee {
    String name;
    int id;

    void work() {
        System.out.println(name + " is working.");
    }
}
```

Houd klassen gefocust op één duidelijke verantwoordelijkheid.

Dit idee is later een basis voor clean architecture.

### 4) Objecten maken

Je maakt objecten met `new`.

```java
Employee emp1 = new Employee();
emp1.name = "Sara";
emp1.id = 101;
emp1.work();
```

Elk object krijgt zijn eigen veldwaarden.

Dus een wijziging in één object verandert meestal niet een ander object, tenzij beide referenties naar hetzelfde object wijzen.

### 5) Geheugentoewijzing

In eenvoudige termen:

- Lokale primitieve waarden worden direct opgeslagen
- Objecten worden aangemaakt in heap-geheugen
- Variabelen zoals `emp1` slaan referenties naar die objecten op

```java
Employee emp1 = new Employee();
Employee emp2 = emp1;
```

Nu wijzen `emp1` en `emp2` naar hetzelfde object in het geheugen.

Zie referenties als twee afstandsbedieningen die gekoppeld zijn aan dezelfde tv.

### 6) Procedureel programmeren

Procedureel programmeren organiseert code vooral als functies/stappen.

OOP organiseert code rond objecten.

Procedurele stijl is prima voor kleine scripts, maar bij grote apps wordt het vaak rommelig omdat data en logica te veel gescheiden raken.

OOP verbetert dit door gerelateerde data + gedrag bij elkaar te houden.

Snelle gebruiksgids:

- procedurele stijl: goed voor kleine scripts en lineaire taken
- OOP-stijl: beter voor systemen met veel gerelateerde entiteiten en regels

### 7) Encapsulatie

Encapsulatie betekent interne details verbergen en toegang controleren via methodes.

Dat doe je vaak door velden `private` te maken.

```java
class Account {
    private double balance;
}
```

Dit voorkomt dat code van buitenaf `balance` op onveilige manieren wijzigt.

Encapsulatie is in de kern gecontroleerde toegang: bescherm interne staat, bied veilige operaties aan.

### 8) Getters en Setters

Getters lezen private velden.  
Setters werken private velden bij met controle/validatie.

```java
class Account {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        if (balance >= 0)
            this.balance = balance;
    }
}
```

Dit beschermt je object tegen ongeldige data.

Gebruik setters wanneer je validatie nodig hebt; stel alleen wijzigingen bloot die veilig zijn voor je businessregels.

### 9) Abstractie

Abstractie betekent tonen wat nodig is en complexe details verbergen.

Bijvoorbeeld: een gebruiker kan `car.start()` aanroepen zonder alle interne stappen van de motor te kennen.

Abstractie maakt code makkelijker te gebruiken en te begrijpen.

Zie abstractie als een autodashboard: je gebruikt pedalen en stuur, niet de details van de motor.

### 10) Coupling

Coupling is hoe sterk klassen van elkaar afhankelijk zijn.

- Hoge coupling = klassen zitten strak aan elkaar vast (moeilijker te wijzigen)
- Lage coupling = klassen zijn onafhankelijker (makkelijker te onderhouden)

Doel: houd coupling zo laag mogelijk waar het kan.

Lagere coupling betekent meestal makkelijker testen en eenvoudiger componenten vervangen.

### 11) Coupling verminderen

Manieren om coupling te verminderen:

- Afhankelijk zijn van interfaces in plaats van concrete klassen
- Dependencies doorgeven via constructors of methodes
- Klassen gefocust houden op één taak

Slecht idee:

```java
class OrderService {
    private EmailService email = new EmailService(); // tightly coupled
}
```

Beter idee:

```java
class OrderService {
    private NotificationService notificationService;

    public OrderService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
}
```

Nu kun je implementaties makkelijker wisselen.

Korte samenvatting:

- hoge coupling = moeilijk te veranderen
- lage coupling = flexibel en onderhoudbaar

### 12) Constructors

Een constructor is een speciale methode die gebruikt wordt bij het maken van objecten.

- Zelfde naam als de klasse
- Geen returntype

```java
class User {
    String name;

    User(String name) {
        this.name = name;
    }
}
```

Wanneer je een `User` maakt, draait de constructor automatisch.

Constructors helpen om te garanderen dat objecten starten in een geldige beginstaat.

### 13) Method Overloading

Method overloading betekent dat je dezelfde methodenaam gebruikt met verschillende parameters.

```java
class Printer {
    void print(String text) {
        System.out.println(text);
    }

    void print(int number) {
        System.out.println(number);
    }
}
```

Java kiest automatisch de juiste versie op basis van de argumenten.

Overloading verbetert leesbaarheid doordat vergelijkbare acties onder één methodenaam blijven.

### 14) Constructor Overloading

Je kunt constructors ook overloaden.

```java
class Product {
    String name;
    double price;

    Product(String name) {
        this.name = name;
    }

    Product(String name, double price) {
        this.name = name;
        this.price = price;
    }
}
```

Dit geeft flexibele manieren om objecten te maken.

Veelgebruikt patroon: bied een eenvoudige constructor en een volledige constructor voor geavanceerde gevallen.

### 15) Static Members

`static` members horen bij de klasse zelf, niet bij elk object.

Gebruik static wanneer data/gedrag gedeeld wordt door alle objecten.

```java
class Employee {
    static int count = 0;

    Employee() {
        count++;
    }
}

System.out.println(Employee.count);
```

Je kunt static members benaderen via de klassenaam, zoals `Employee.count`.

Korte samenvatting:

- instance members horen bij elk object
- static members horen bij de klasse zelf
- gebruik static voor gedeelde utilities of gedeelde counters

Hoe dit samenhangt:

- Deze sectie leert de kernbouwstenen (classes, objects, encapsulatie, constructors).
- Daarna laat refactoring zien hoe je rommelige code verbetert met juist deze bouwstenen.

---

## Refactoring naar een Object-oriented Ontwerp

### 1) Introductie

In deze sectie is het doel niet alleen om code te laten werken - het doel is ook om code schoon, herbruikbaar en objectgeoriënteerd te maken.

Je neemt een werkend programma en verbetert stap voor stap het ontwerp.

Zie refactoring als een kamer opruimen en opnieuw indelen: dezelfde kamer, maar makkelijker te gebruiken en onderhouden.

Korte samenvatting:

- refactoring verandert de structuur, niet het gedrag
- doel is leesbaarheid, hergebruik en onderhoudbaarheid
- kleine veilige stappen zijn beter dan één grote herschrijving

Overeenkomst tussen ontwerpprincipes:

- separation of concerns splitst verantwoordelijkheden
- cohesion houdt gerelateerde code bij elkaar
- lage coupling maakt onderdelen vervangbaar

Refactoring brengt deze principes stap voor stap in je code.

### 2) Het Probleem

Veel beginnersprogramma's beginnen met alles in één grote `main`-methode.

Dat werkt in het begin, maar het wordt lastig om:

- de code te lezen
- onderdelen apart te testen
- logica te hergebruiken
- één ding aan te passen zonder iets anders stuk te maken

Dit is precies waar refactoring helpt.

Snelle gebruiksgids:

- als een methode te lang wordt, splits verantwoordelijkheden op
- als code zich herhaalt, extraheer helper-methodes
- als namen onduidelijk zijn, hernoem op intentie

### 3) Welke Klassen Hebben We Nodig?

Een goede eerste refactorvraag is:

"Welke verantwoordelijkheden bestaan er in dit programma?"

Voor een mortgage-app zijn veelvoorkomende verantwoordelijkheden:

- Gebruikersinvoer lezen
- Mortgage-berekeningen uitvoeren
- Rapporten tonen

Dat leidt tot klassen zoals:

- `Console` (invoer/output)
- `MortgageCalculator` (rekenlogica)
- `MortgageReport` (weergave/rapportopmaak)

Dit heet separation of concerns: elke klasse behandelt één hoofdverantwoordelijkheid.

### 4) De Console-klasse Extraheren

In plaats van invoer direct in `main` te lezen, verplaats je die logica naar een `Console`-klasse.

```java
class Console {
    public static double readNumber(String prompt) {
        System.out.print(prompt);
        return new java.util.Scanner(System.in).nextDouble();
    }
}
```

Nu wordt `main` schoner en makkelijker te volgen.

Zie `main` als een orchestrator, niet als plek voor alle detaillogica.

### 5) Methodes Overloaden

Overloading is nuttig wanneer je vergelijkbaar gedrag wilt met verschillende invoer.

Voorbeeld in `Console`:

```java
class Console {
    public static double readNumber(String prompt) { /* ... */ return 0; }
    public static double readNumber(String prompt, double min, double max) { /* ... */ return 0; }
}
```

Dit helpt invoer te valideren zonder logica te herhalen.

Overloading houdt één duidelijke methodenaam terwijl je meerdere gebruiksscenario's ondersteunt.

### 6) De MortgageReport-klasse Extraheren

Het afdrukken van schema/rapport is een aparte verantwoordelijkheid van berekeningen.

Verplaats rapportcode naar `MortgageReport`.

```java
class MortgageReport {
    public void printMonthlyPayment(double payment) {
        System.out.println("MONTHLY PAYMENTS");
        System.out.println("----------------");
        System.out.println(payment);
    }
}
```

Dit houdt presentatiecode op één plek.

Een goede ontwerpgewoonte: houd "rekenlogica" en "weergavelogica" gescheiden.

### 7) De MortgageCalculator-klasse Extraheren

Alle mortgage-formules horen in een toegewijde klasse.

```java
class MortgageCalculator {
    private final int principal;
    private final float annualInterest;
    private final byte years;

    public MortgageCalculator(int principal, float annualInterest, byte years) {
        this.principal = principal;
        this.annualInterest = annualInterest;
        this.years = years;
    }
}
```

Deze klasse wordt de single source of truth voor mortgage-wiskunde.

Single source of truth vermindert bugs omdat formules op één plek staan.

### 8) Wegbewegen van Static Members

In het begin zijn static methodes handig. Maar te veel static-gebruik maakt code star.

Objectgeoriënteerd ontwerp geeft de voorkeur aan instance-methodes wanneer logica afhangt van objectstaat.

Betere richting:

- maak een object met constructor-data
- roep instance-methodes aan zoals `calculator.calculateMortgage()`

Dit verbetert testbaarheid en flexibiliteit.

Instance-gebaseerd ontwerp is makkelijker te testen omdat elk object een eigen staat kan hebben.

### 9) Static Velden Verplaatsen

Constanten die bij een klasse horen, moeten in die klasse blijven.

```java
class MortgageCalculator {
    private static final byte MONTHS_IN_YEAR = 12;
    private static final byte PERCENT = 100;
}
```

Dit verbetert cohesion (wat bij elkaar hoort, blijft bij elkaar).

Cohesion betekent dat code die samenhoort ook samen blijft.

### 10) Dubbele Logica Extraheren

Als je dezelfde formule in twee methodes herhaalt, extraheer die dan één keer.

Voor:

- formule voor maandrente herhaald
- formule voor aantal betalingen herhaald

Na:

```java
private float getMonthlyInterest() {
    return annualInterest / PERCENT / MONTHS_IN_YEAR;
}
```

Dit vermindert fouten en maakt updates makkelijker.

Als een formule later verandert, pas je één methode aan in plaats van veel kopieën.

### 11) getRemainingBalances Extraheren

Bij het maken van een betalingsschema heb je vaak veel saldowaarden nodig.

In plaats van loops en printlogica overal te mengen, extraheer je een methode:

```java
public double[] getRemainingBalances() {
    double[] balances = new double[years * MONTHS_IN_YEAR];
    for (short month = 1; month <= balances.length; month++)
        balances[month - 1] = calculateBalance(month);
    return balances;
}
```

Nu kan rapportcode focussen op weergave, niet op berekeningen.

Dit is een sterk teken van schoon ontwerp: elke methode/klasse heeft één duidelijke taak.

### 12) Een Laatste Touch

Na de hoofdrefactoring doe je een laatste opschoonronde:

- hernoem onduidelijke variabelen
- verbeter methodenamen
- verwijder dode code
- houd opmaak consistent

Deze kleine touches verbeteren de leesbaarheid enorm.

Eindpolish is waar "werkende code" verandert in "professionele code".

### 13) Een Korte Opmerking

Refactoring is geen eenmalige actie. Het is een gewoonte.

Een sterke workflow is:

1. Laat het werken
2. Refactor om het ontwerp te verbeteren
3. Houd het gedrag hetzelfde
4. Herhaal in kleine, veilige stappen

Zo ga je van "code die draait" naar "code die professioneel en onderhoudbaar is."

Herhaalbare korte workflow:

1. laat het werken
2. verwijder duplicatie
3. verbeter naamgeving
4. scheid verantwoordelijkheden
5. verifieer dat gedrag ongewijzigd is

Hoe dit samenhangt:

- Refactoring geeft je praktische ontwerpgewoontes.
- Inheritance (volgende) voegt hergebruik toe tussen gerelateerde klassen.

---

## Inheritance

### 1) Introductie

Inheritance laat één klasse velden en methodes van een andere klasse hergebruiken.

Het helpt je herhaling vermijden en "is-a"-relaties te modelleren, zoals `Dog` is een `Animal`.

Zie inheritance als een stamboom: child-klassen erven gemeenschappelijke eigenschappen van parent-klassen.

Korte samenvatting:

- parent class = gedeeld gedrag
- child class = gespecialiseerd gedrag
- inheritance modelleert "is-a"-relaties

Overeenkomst tussen inheritance-concepten:

- overriding geeft kindspecifiek gedrag
- polymorfisme gebruikt dat gedrag via parent-referenties
- abstracte klassen combineren gedeelde basis met verplichte implementatie

Deze drie werken samen om herbruikbare en uitbreidbare hiërarchieën te maken.

### 2) Inheritance

Een child-klasse breidt een parent-klasse uit met `extends`.

```java
class Animal {
    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking...");
    }
}
```

`Dog` heeft nu zowel `eat()` als `bark()`.

Gebruik inheritance wanneer child echt een gespecialiseerd type van parent is, niet alleen omdat code op elkaar lijkt.

### 3) De Object-klasse

In Java erft elke klasse direct of indirect van `Object`.

Dat betekent dat elk object standaardmethodes heeft zoals:

- `toString()`
- `equals()`
- `hashCode()`

Dus zelfs je eigen klassen erven automatisch gemeenschappelijk gedrag.

Daarom zijn methodes zoals `toString()` beschikbaar op alle objecten.

### 4) Constructors en Inheritance

Wanneer je een child-object maakt, draait eerst de constructor van de parent.

```java
class Animal {
    Animal() {
        System.out.println("Animal constructor");
    }
}

class Dog extends Animal {
    Dog() {
        System.out.println("Dog constructor");
    }
}
```

Dit zorgt ervoor dat parent-state geïnitialiseerd is vóór child-specifieke logica.

Constructorvolgorde is belangrijk omdat child-logica kan afhangen van parent-velden die al klaar moeten zijn.

### 5) Access Modifiers

Access modifiers bepalen zichtbaarheid:

- `private` - alleen binnen dezelfde klasse
- `protected` - zelfde package + subclasses
- `public` - overal
- (geen modifier) - package-private

Bij inheritance is `protected` vaak nuttig wanneer children gecontroleerde toegang nodig hebben.

Snelle gebruiksgids:

- houd velden standaard `private`
- gebruik `protected` alleen wanneer subclass-toegang echt nodig is
- maak niet alles `public`

### 6) Methodes Overschrijven (Overriding)

Een child-klasse kan een eigen versie geven van een parent-methode.

```java
class Animal {
    void speak() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    void speak() {
        System.out.println("Woof");
    }
}
```

Gebruik `@Override` om intentie duidelijk te maken en fouten te vangen.

Overriding is hoe polymorfisme praktisch wordt in echte code.

### 7) Upcasting en Downcasting

- **Upcasting**: child -> parent (veilig, automatisch)
- **Downcasting**: parent -> child (expliciete cast nodig, kan falen)

```java
Animal a = new Dog(); // upcasting
Dog d = (Dog) a;      // downcasting
```

Downcast alleen wanneer je zeker weet dat het object dat child-type echt is.

Veilig patroon:

```java
if (a instanceof Dog) {
    Dog d = (Dog) a;
}
```

### 8) Objecten Vergelijken

`==` vergelijkt referenties (zelfde object in geheugen).  
`equals()` vergelijkt inhoud/betekenis (als correct overschreven).

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2);      // false
System.out.println(s1.equals(s2)); // true
```

Voor custom classes override je `equals()` (en meestal `hashCode()`) voor waardegebaseerde vergelijking.

Als twee objecten dezelfde logische waarde voorstellen, moet `equals()` dat weerspiegelen.

### 9) Polymorfisme

Polymorfisme betekent dat één parent-referentie naar meerdere child-types kan wijzen.

```java
Animal[] animals = { new Dog(), new Cat() };
for (Animal animal : animals)
    animal.speak();
```

Elke child draait zijn eigen `speak()`-versie.  
Dit is krachtig voor flexibel en uitbreidbaar ontwerp.

Polymorfisme laat je één loop/algoritme schrijven dat met veel child-gedragingen werkt.

### 10) Abstracte Klassen en Methodes

Een abstracte klasse kun je niet direct instantieren.  
Het is een sjabloon voor child-klassen.

```java
abstract class Shape {
    abstract double area();
}
```

Child-klassen moeten abstracte methodes implementeren.

Abstracte klassen zijn handig als je gedeelde basiscodestructuur wilt plus verplicht child-specifiek gedrag.

### 11) Final Klassen en Methodes

- `final class` kan niet uitgebreid worden
- `final method` kan niet overschreven worden

```java
final class SecurityManager {
}
```

Gebruik `final` wanneer gedrag vast moet blijven.

`final` is een beschermingstool: het voorkomt per ongeluk of onveilig uitbreiden/overschrijven.

### 12) Diepe Inheritance-hiërarchieën

Te veel inheritance-niveaus maken code moeilijk te begrijpen en onderhouden.

Houd hiërarchieën liever ondiep en duidelijk.  
Als inheritance te complex wordt, overweeg composition (objecten in objecten gebruiken).

### 13) Multiple Inheritance

Java staat multiple inheritance van klassen niet toe.

Dit mag niet:

```java
// class C extends A, B { } // invalid in Java
```

Maar Java ondersteunt wel meerdere interfaces implementeren.

Dit geeft multiple-behavior contracts zonder ambigu parent-state.

### 14) Inheritance Quiz

Snelle zelfcheck:

1. Wat erft een klasse van `Object`?
2. Wat is het verschil tussen overriding en overloading?
3. Waarom is downcasting risicovol?
4. Wanneer gebruik je `final`?
5. Waarom kunnen diepe hiërarchieën problematisch zijn?

Als je deze duidelijk kunt beantwoorden, zijn je inheritance-basics sterk.

### 15) Samenvatting

Inheritance helpt je om:

- code te hergebruiken
- echte relaties te modelleren
- polymorfisme te ondersteunen

Gebruik het bewust:

- houd hiërarchieën duidelijk en ondiep
- override met aandacht
- combineer met encapsulatie en abstractie

Goed toegepast maakt inheritance objectgeoriënteerde code schoner en beter onderhoudbaar.

Snelle gebruiksgids:

- gebruik inheritance voor echte "is-a"-modellering
- houd hiërarchieën ondiep
- kies composition als inheritance geforceerd begint te voelen

Korte samenvatting:

- inheritance deelt code tussen gerelateerde types
- overriding past gedrag aan
- polymorfisme maakt parent-gebaseerd programmeren flexibel

Hoe dit samenhangt:

- Inheritance deelt gedrag tussen gerelateerde klassen.
- Interfaces (volgende) delen contracts tussen mogelijk niet-gerelateerde klassen.
- Samen vormen ze de ruggengraat van flexibel OOP-ontwerp.

---

## Interfaces

### 1) Introductie

Interfaces zijn een van de belangrijkste tools in objectgeoriënteerd Java-ontwerp.

Ze helpen klassen samenwerken via contracts, niet via hardgecodeerde implementaties.

Zie een interface als een stopcontactstandaard: veel apparaten kunnen aansluiten zolang ze dezelfde vorm volgen.

Korte samenvatting:

- interface definieert vereist gedrag
- klassen geven concrete implementatie
- dit geeft lage coupling en makkelijker vervangbaarheid

Overeenkomst tussen interface-concepten:

- interfaces definiëren contracten
- dependency injection levert implementaties aan
- interface segregation houdt contracten klein en gericht

Samen maken ze code beter testbaar, verwisselbaar en schaalbaar.

### 2) Wat zijn Interfaces

Een interface is een contract dat definieert wat een klasse moet doen, zonder te zeggen hoe.

```java
interface TaxCalculator {
    double calculateTax();
}
```

Elke klasse die `TaxCalculator` implementeert, moet `calculateTax()` aanbieden.

Dus de rest van je app kan afhangen van het contract, niet van één specifieke calculator-klasse.

### 3) Tight Coupling

Tightly-coupled code ontstaat wanneer een klasse direct afhangt van een specifieke concrete klasse.

```java
class Store {
    private TaxCalculator2024 calculator = new TaxCalculator2024();
}
```

Dit is moeilijk te veranderen en moeilijk te testen.  
Interfaces helpen die strakke koppeling te verminderen.

Tight coupling betekent vaak:

- meer code breekt als één klasse verandert
- moeilijker unit-testen
- minder flexibiliteit voor toekomstige ontwerpwijzigingen

### 4) Een Interface Maken

Maak een interface met `interface`, en implementeer die in klassen.

```java
interface NotificationService {
    void send(String message);
}

class EmailService implements NotificationService {
    public void send(String message) {
        System.out.println("Email: " + message);
    }
}
```

Nu kan je code werken met `NotificationService` in plaats van één specifieke klasse.

Dit is het kernidee van OOP-ontwerp: afhankelijk zijn van abstracties, niet van concrete details.

### 5) Dependency Injection

Dependency Injection betekent dat je benodigde objecten van buitenaf doorgeeft in plaats van ze binnen een klasse te maken.

Dit verlaagt coupling en maakt code makkelijker te testen.

Dependency injection is hoe interfaces praktisch worden in echte applicaties.

### 6) Constructor Injection

Geef dependency door via constructor.

```java
class OrderService {
    private final NotificationService notificationService;

    public OrderService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
}
```

Dit is de meest voorkomende en vaak beste injectiestijl.

Constructor injection heeft voorkeur omdat vereiste dependencies meteen aanwezig zijn.

### 7) Setter Injection

Geef dependency door via een setter-methode.

```java
class OrderService {
    private NotificationService notificationService;

    public void setNotificationService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
}
```

Handig wanneer dependency optioneel is of later kan veranderen.

Gebruik setter injection bewust; te veel optionele dependencies maken object-state onduidelijk.

### 8) Method Injection

Geef dependency direct mee aan de methode die ze nodig heeft.

```java
class OrderService {
    public void placeOrder(NotificationService notificationService) {
        notificationService.send("Order placed.");
    }
}
```

Goed wanneer dependency maar in één operatie gebruikt wordt.

Method injection houdt dependency-scope heel lokaal.

### 9) Interface Segregation Principle

Dit principe zegt: dwing klassen niet om methodes te implementeren die ze niet nodig hebben.

Slecht ontwerp:

```java
interface Worker {
    void work();
    void eat();
}
```

Beter ontwerp: splits in kleinere interfaces.

```java
interface Workable { void work(); }
interface Eatable { void eat(); }
```

Kleine, gerichte interfaces houden code schoner.

Eenvoudige regel: meerdere kleine gerichte interfaces zijn meestal beter dan één grote "doe-alles"-interface.

### 10) Project - MyTube Video Platform

Stel je voor dat je een eenvoudige YouTube-achtige app bouwt.

Hoofdflow:

1. Video encoden
2. Video-metadata opslaan
3. Gebruiker notificeren

Een perfecte plek om interfaces te gebruiken:

- `VideoEncoder`
- `VideoDatabase`
- `NotificationService`

### 11) Oplossing

Een serviceklasse kan van interfaces afhangen:

```java
class VideoProcessor {
    private final VideoEncoder encoder;
    private final VideoDatabase database;
    private final NotificationService notifier;

    public VideoProcessor(VideoEncoder encoder, VideoDatabase database, NotificationService notifier) {
        this.encoder = encoder;
        this.database = database;
        this.notifier = notifier;
    }
}
```

Je kunt implementaties wisselen zonder `VideoProcessor` te wijzigen.

Dat is een grote onderhoudswinst naarmate systemen groeien.

### 12) Velden

Interfacevelden zijn altijd:

- `public`
- `static`
- `final`

Dus het zijn constanten.

```java
interface Tax {
    double MIN_TAX = 1000;
}
```

Interfaces zijn niet bedoeld voor instance-state; ze zijn vooral gedrag-contracten.

### 13) Static Methodes

Interfaces kunnen static methodes hebben (Java 8+).

```java
interface Logger {
    static void log(String message) {
        System.out.println("[LOG] " + message);
    }
}
```

Aanroepen doe je met interfacenaam: `Logger.log("Started");`

Static interface-methodes zijn utility-achtige helpers die bij het interfaceconcept horen.

### 14) Private Methodes

Interfaces kunnen ook private helpermethodes hebben (Java 9+), intern gebruikt door default/static methodes.

```java
interface Greeting {
    default void sayHi() {
        print("Hi");
    }

    private void print(String text) {
        System.out.println(text);
    }
}
```

Dit voorkomt herhaling van helperlogica in de interface.

Private interface-methodes helpen default/static methodes DRY te houden.

### 15) Interfaces en Abstracte Klassen

Gebruik interfaces voor contracts.  
Gebruik abstracte klassen voor gedeelde basiscode/state.

Snelle regel:

- Meerdere contracts nodig? -> interfaces
- Gedeelde velden + gedeeltelijke implementatie nodig? -> abstracte klasse

Beide kunnen samen in één ontwerp gebruikt worden.

Denk:

- interface = "wat moet er gebeuren"
- abstracte klasse = "gedeelde gedeeltelijke manier om het te doen"

### 16) Wanneer Gebruik je Interfaces

Gebruik interfaces wanneer:

- Je lage coupling wilt
- Je implementaties makkelijk wilt wisselen
- Je makkelijker unit-tests wilt (mocken van dependencies)
- Meerdere klassen hetzelfde contract moeten volgen

Voeg interfaces niet toe "omdat het moet".  
Gebruik ze wanneer ze flexibiliteit en duidelijkheid verbeteren.

Snelle gebruiksgids:

- begin met eenvoudige concrete klassen
- introduceer interfaces wanneer meerdere implementaties of testflexibiliteit nodig is

### 17) Veelgemaakte Beginnersfouten

Let op deze:

- Te vroeg interfaces maken bij één kleine klasse zonder echte flexibiliteitsbehoefte
- Te veel ongerelateerde methodes in één interface stoppen
- Afhankelijk blijven van concrete klassen in servicelagen

Begin simpel en introduceer interfaces waar ze een echt ontwerpprobleem oplossen.

Vermijd interfaces als "extra ceremonie" zonder concreet voordeel.

### 18) Oefencheck

Probeer deze korte oefening:

1. Maak een interface `PaymentGateway` met `processPayment(double amount)`
2. Implementeer `StripeGateway` en `PayPalGateway`
3. Injecteer één van beide in `CheckoutService`
4. Wissel implementatie zonder `CheckoutService` te wijzigen

Als dit duidelijk voelt, zijn je interface-basisvaardigheden sterk.

### 19) Samenvatting

Interfaces helpen je flexibele en onderhoudbare OOP-systemen te ontwerpen.

Belangrijkste ideeën:

- Programmeer tegen interfaces, niet tegen implementaties
- Gebruik dependency injection om coupling te verlagen
- Houd interfaces klein en gefocust
- Combineer interfaces met OOP-principes voor schoner ontwerp

Korte samenvatting:

- interfaces definiëren contracts
- dependency injection verbindt contracts met implementaties
- kleine gefocuste interfaces verbeteren onderhoudbaarheid

Hoe dit samenhangt:

- Interfaces vullen inheritance aan: inheritance deelt implementatie, interfaces delen contracten.
- Met dependency injection combineer je beide voor flexibel, testbaar ontwerp.
