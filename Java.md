# Java 8

## Language Basics

### Variables

Java definisce i seguenti tipi di variabili:
* **Variabili di istanza** (campi non statici) i loro valori sono unici per ogni
istanza di una classe.

* **Variabili di classe** (campi statici) è un qualsiasi campo dichiarato statico.
Questo dice al compilatore che c’è esattamente una copia di questa variabile,
indipendentemente da quante volte la classe è stata istanziata. Se aggiungiamo
la keyword final indichiamo che la variabile non verrà cambiata.

* **Variabili locali** simile a come un oggetto memorizza il suo stato nei campi dati, un metodo
spesso memorizza il suo stati temporaneo in variabile locali. Una variabile locale è visibile
solo nel metodo in cui è stata dichiarata.

* **Parametri**: sono variabili argomenti di un metodo.

### Primitive Data Types

Java è statically-typed, cioè tutte le variabili devono essere dichiarate prima di essere usate.
Java supporta **8 primitive data types**. Un tipo primitivo è un tipo predefinito del linguaggio:

* **byte** intero in complemento a due con segno a 8 bit. Valore minimo -128 e massimo +127.
* **short** intero in complemento a due con sengo a 16 bit. Valore minimo -32_768 e massimo + 32_767.
* **int** intero in complememto a due con segno a 32 bit. Valore minimo n^2
* **long**
* **float**
* **double**
* **boolean**
* **char**

In aggiunta a questi 8 tipi primitivi Java fornisce un supporto speciale per le stringhe di carattere
attraverso la classe `java.lang.String`.
Inserendo una stringa di caratteri all'interno di doppie virgolette verrà automaticamente creata un
nuovo oggetto `String`. Gli oggetti di tipo `String` sono immutabili: una volta creati il loro valore
non può essere cambiato. La class `String` non è tecnicamente un tipo di dato primitivo.


#### Default Values
Data Type  | Default value
-----------|--------------
byte       |  0
short      |  0
int        |  0
long       |  0L
float      |  0.0f
double     |  0.0d
char       |  \u0000
String     |  null
boolean    | false

> **NB**: Per le variabili locali il compilatore non assegna mai un valore di default, perciò prima di
usarle ricordati sempre di inizilizzarle. Accedere ad una variabile locale non inizializzata
produce un errore di compilazione.

## Classes and Objects

### Classes

#### Declaring Classes

Dichiarazione di una classe

```java
class MyClass {
  // campi dati, costruttore, dichiarazione metodi
}

class MyClass extends MySuperClass implements YourInterface {
  // campi dati, costruttore, dichiarazione metodi
}
```

#### Methods

I metodi hanno 6 componenti:

1. Modificatori
2. Tipo di ritorno
3. Nome del meotodo
4. Lista di parametri
5. Lista di eccezzioni
6. Corpo del metodo


**Definizione**: Due dei componenti di una dichiarazione di un metodo costituiscono la firma del
metodo, il nome del metodo e il tipo dei parametri**

#### Overloading Methods

Overloading == metodo con stesso nome.
Java può distinguere tra due metodi con firme differenti. Ciò significa che metodi in una Classe
possono avere lo stesso nome se hanno una differente lista di parametri. Il tipo di ritorno non ha influenza.

#### Constructors

Metodo senzaa tipo di ritorno e con lo stesso nome della classe. Se non dichiaro costruttori è
disponibile il costruttore di default che invoca il costruttore senza parametri della supercalsse
diretta. Se la supercalsse diretta non ha un costruttore di default verrà segnalato un errore
dal compilatore. Se invece non ha una superclasse esplicità verrà invocato il costruttore di
default dell classe `Object`.

#### Arbitrary Number of Arguments

È possibile usare un costrutto chiamato `varargs` per passare un numero arbitrario ad un metodo.
Si usa quando non si conosce il numero di quanti argomenti di un unico tipo saranno passati
al metodo. È un abbrevizione alla creazione di un array creato manualmente.

```java
public void fun(int... i) {
  int numberOfIneger(i.lenght);
}
```

#### Passing Primitive Data Type Arguments

Argomenti primitivi sono passati per valore. Ciò significa che qualsiasi modifica al valore
del parametro esiste solo nello scope del metodo.

#### Passing Reference Data Type Arguments

I reference, come gli oggetti, sono passati per valore. Questo significa che quando il metodo ritorna,
il riferimento passato continua a riferirsi allo stesso oggetto di prima. Tuttavia i valori dei campi
dell'oggetto possono essere modificati nel metodo, se hanno il livello di accesso appropriato.

### Objects

#### Creating Objects

```java
Point MyPoint = new Point(23,94);
```
Questo statement è costituito da tre parti:

* **Dichiarazione**
* **Instanziazione**
* **Inizializzazione**

##### Declaring a Variable to Refer to an Object

Una dichiarazione associa un nome di variabile con un tipo di oggetto.

`type name`

Questo notifica al compilatoreche userai `name` per riferirti ad un oggetto che ha tipo `type`.
Il valore di name sarà indeterminato fino a quando un oggetto sarà effetivamente creato e
assegnato  ad esso. Dichiarare un varibile riferimento non crea un oggetto.



##### Instantiating a Class

L'operatore `new` instanzia una classe allocando la memoria per un nuovo oggetto e ritorna un
riferimento a quell'area di memoria. Invoca anche il costruttore dell'oggetto.

> **istanziare una classe**  significa **creare un oggetto**. Quando crei un oggetto stai creando
> un istanza di una classe.

L'operatore `new` richiede un singolo argomento postfisso: una chiamata al costruttore.
L'operatore `new` ritorna un riferimento all'oggetto creato. Questo riferimento è solitamente
assegnato ad una variabile del tipo appropriato.
Il reference restituito dall'operatore `new ` non deve necessariamente essere assegnato ad una
variabile ma può essere usato direttamente:

```java
int height = new MyPoint().height;
```

##### Initializing an Object

L'operatore `new` è seguito da una chiamata al construttore il quale inizializza il nuovo
oggetto.


### More On Classes

#### Garbage Collector

Un oggetto è eleggibile per il garabage collector quando non è più riferito da alcuna variabile.


#### Using the this Keyword

In un metdodo di istanza o in un costruttore `this` è un riferimento all'oggetto corrente, ossia
l'oggeto su cui viene chiamato il metodo o il costruttore.

All'interno di un costruttore si può usare la keyword `this` per chiamare un altro costruttore
nella stessa classe. Si tratta di una chiamata esplicita al costruttore.


#### Controlling Access to Members of a Class

I modificatori del livello di accesso determinano se un'altra classe può usare un particolare
campo o invocare un particolare metodo. Ci sono due livelli di controllo d'accesso:

* Al livello più alto (classe): `public` oppure package-private (senza modificatori espliciti).
* A livello di membri (campi dati o metodi): `public, private, protected` oppure package-private
(senza modificatori espliciti).

Se una classe è marcata `public` allora può essere acceduta da qualsiasi altra classe. Se una
classe non ha modificatori è visibile solo all'interno del suo package.

Per i membri di una classe, il comportamento di `public` e di nessun modificatore è identico a
quello di una classe. Per i membri ci sono 2 modificatori aggiuntivi:

* `private` specifica che il membro può essere acceduto nella sua stessa classe.
* `protected` specifica che un membro può essere acceduto all'interno dello stesso package e da
una sottoclasse della classe in questione anche se si trova in un altro package.


**Acces Level**

Modificatore  | Classe  |Package   |Sottoclasse   |  Mondo
--------------|---------|----------|--------------|--
public        | Y       |  Y       | Y            |  Y
protected     | Y       |  Y       | Y            |  N
blank              | Y       |  Y       | N            |  N
private       | Y       |  N       | N            |  N


La prima colonna indica se la classe stessa ha accesso al membro definito dal livello di accesso.
Una classe ha sempre accesso ai propri membri (tutto Yes).
La seconda colanna indica se le classi nello stesso package della classe hanno accesso al membro.
La terza colonna indica se le sottoclassi della classe dichiarate all'esterno di questo pacchetto
hanno accesso al membro.
La quarta colonna indica se tutte le classi hanno accesso al membro.

**Tips on Choosing an Acces Level**

Usa il modificatore di accesso più restrittivo che abbia senso per un particolare membro.
* Usa`private` a meno che non ci sia un buon motivo per non farlo.
* Evita i campi `public` eccetto che per le costanti.

I campi marcati `public` tendono a vincolarti ad una particolare implementazione e limitare la
in flessibilità nel modificare il codice.

#### Understanding Class Members


##### Class Variables [static]

Campi dati dichiarati `static` sono chiamati campi dati statici o variabili di classe.
Sono associati alla classe invece che ad un oggetto. Ogni istanza di una classe condivide una
variabile di classe, la quale si trova in una regione fissa di memoria. Ogni oggetto può
cambirare il valore di una variabile di classe, ma le variabile di classe possono essere
manipolate anche senza creare un istanza di quella classe.

Le variabili di classe sono referenziate dal nome della classe:

```java
ClassName.staticVariable;
```

##### Class Methods [static]

I metodi statici, come per le variabili di classe, dovrebbero essere invocati con il nome
della classe:

```java
ClassName.methodName(args);
```

Un uso comune dei metodi statici è quello di accedere ai campi dati statici.
Non tutte le combinazioni di variabili di classe, di istanza e di metodi sono permesse:

* Metodi di istanza possono accedere variabili di istanza e metodi di istanza direttamente.
* Metodi di istanza possono accedere variabili statiche e metodi statici direttamente.
* Metodi statici possono accedere variabili statiche e metodi statici direttamente.
* Metodi statici non possono accedere variabili d'istanza o metodi di istanza direttamente.
Devono usare un riferimento ad un oggetto. Inoltre, i metodi statici non possono usare la keyword
`this` in quanto non vi è alcuna istanza a cui fare riferimento.

##### Constants

Il modificatore `final` indica che il valore di quel campo **non** può cambiare.
Il modificatore `static` in combinazione a `final`, viene usato per definire costanti.

```java
static final double PI = 3.1415;
```

Costanti definite in questo modo non possono più essere riassegnate in quanto tipo primitivo. Se fosse un oggetto sarebbe immutabile il reference ma non l'oggetto puntato.

> **nota:** se un tipo primitivo o una stringa è difinito come costante ed il suo valore è conosciuto a tempo di compilazione, il compilatore sostituisce ovunque i nomi delle costanti nel codice con il loro valore. Questo meccanismo si chiama **compile-time constant**. Se il valore della costante all'esterno cambia, bisogna ricompilare tutte le classi che usano questa costante per ottenere il nuovo valore.



#### Initializing Fields

È possibile fornire un valore iniziale per un campo nella sua dichiarazione:

```java
// initialize to 10
public static int capacity = 10;

// intialize to false
private boolean full = false;
```

Se un inizializzazione richede della logica, una semplice assegnazione risulta inadeguata.
Le variabili di istanza possono essere inizializzate nei ccostruttori, dove si può usare
la gestione degli errori o altra logica.

Per fornire le stessa capacità alle variabili di classe, Java include dei blocchi di
inizializzazione statica.

##### Static Initialization Blocks

un blocco di inizializzazione statica è un normale blocco di codice racchiuso tra due `{ ... }`.


```java
static {
  // code here fot init...
}
```

Una classe può avere qualsiasi numero di blocchi di inzializzazione statico, e possono apparire
in qualsiasi punto del corpo della classe. Il sistema a runtime garantisce che i blocchi di
inizializzazione statica sono chiamati nell'ordine in cui appaiono nel codice.


##### Initializing Instance Members

Solitamente inizializziamo una variabile d'istanza nel costruttore.
Ci sono due alternative nell'usare un costruttore per inizilizzare una variabile d'istanza:

* blocchi di Inizializzazione
* metodi final

I blocchi di inizializzazione sono come i blocchi di inizializzaione statica ma senza la
keyword `static`:

```java
{
  //code here for init ...
}
```

>Il compilatore Java copia i blocchi di inizializzazione in ogni costruttore. Pertanto questo
>approccio può essere usato per condividere un blocco di codice tra più costruttori.

Un metodo marcato `final` non può essere overriden in una sottoclasse. #vedi interfacce ed
ereditarietà.

### Nested Classes

Java consente la creazione di classi interne

```java
class OuterClass {
  ...
  class NestedClass {
    ...
  }
}
```

Le classi nidificate sono divise in due categorie:

* statiche (static nested class)
* non statiche (inner class)

```java
class OuterClass {
  ...
  static class StaticNestedClass {
    ...
  }
  class InnerClass {
    ...
  }
}
```

Una classe nidificata è un membro della classe esterna. Le classi nidificate non statiche (classi interne) hanno accesso ad altri membri della classe esterna, anche se dichiarati `private`. Le classi nidificate statiche non hanno accesso ai membri della classe esterna. In quanto membro della
classe esterna una classe nidificata può essere dichiarata `private`, `public`, `protected`, o
senza modificatori cioè package private.

#### Why Use Nested Classes?

Validi motivi per usare le classi nidificate sono:

* È un modo per raggruppare logicamente classi che sono usate solamente in un posto: Se una classe
è utile solo per un altra classe, allora è logico integrarla nell'altra classe e tenerle insieme.

* Aumenta l'ncapsulamento: Supponiamo due classi di primo livello A e B. Se B ha bisogno di accedere ai membri di A devono essere dichiarati pubblici. Nascondendo la classe B all'interno di A i membri di A possono essere dichiarati privati e B può accedervi. Inoltre B è nascosta dal mondo esterno.

* Può portare a un codice più leggibile e gestibile: L'inserimento di classi di piccole dimensioni all'interno di una classe di alto livello avvicina il codice a dove viene utilizzato.

#### Inner Classes

Come per i metodi e le varibili di istanza, una classe interna è associata ad un'istanza della classe esterna e ha accesso diretto ai metodi e ai campi di quell'oggetto. Inoltre, poichè una classe interna è associata ad un'istanza, non può definire alcun membro statico.

Oggetti istanziati da una classe interna **esistono** all'interno di un'istanza della classe esterna:

```java
class OuterClass {
  ...
  class InnerClass {
    ...
  }
}
```

Un istanza di una classe interna può esistere solo all'interno di un'istanza di una classe esterna e ha accesso diretto ai metodi e ai campi dell'istanza della classe esterna.

>In pratica, un oggetto di una classe interna possiede un riferiemento all'oggetto della classe esterna che lo ha creato, un _outerThis_.

Per riferirsi esplicitamente ad un membro della classe esterna si può usare il riferimento _outerThis_ con sintassi:

```java
OuterClass.this.fun() // fun della classe esterna;
OuterClass.this.var = "outerVar" // campo dati classe esterna
```

Dalla classe esterna è possibile accedere a tutti i membri della classe interna ma solo tramite un istanza dell'oggetto della classe interna.

Dall'esterno, per istanziare una classe interna, bisogna prima istanziare la classe esterna, poi creare l'oggetto della classe interna usando l'oggetto della classe esterna:

```java
OuterClass.InnerClass innerObj = outerObj.new InnerClass();
```

Esistoni due tipi speciali di classe interne (non statiche):

* classi locali
* classi anonime


#### Static Nested Classes

Una classe nidificata statica è usata quando non è necessario avere un riferimento ad un oggetto della classe che la contiene. In questo caso rappresenta un tipo logicamente correlato con la classe esterna.

Come per i metodi e le variabili di classe (statiche), una classe statica nidificata è associata alla sua classe esterna. E come per i metodi statici, una classe statica nidificata non può riferirsi direttamente alle variabile di istanza o ai metodi definiti nella classe esterna (non possiede l'_outerThis_): può usarli solo attraverso un riferimento ad un oggetto.

> Una classe statica nidificata interagisce con i membri di istanza della sua classe esterna proprio come qualsiasi altra classe di livello superiore. In effetti, una classe statica nidificata è comportamentalmente una classe di livello superiore che è stata nidificata in un'altra classe di livello superiore per la convenienza del packaging.



Si accede ad una classe statica nidificata usando il nome della classe esterna:

```java
OuterClass.StaticNestedClass
```

Per esempio per creare un oggetto della classe statica nidificata:

```java
OuterClass.StaticNestedClass nestedObj = new OuterClass.StaticNestedClass();
```

##### Shadowing

Se una dichiarazione di un tipo (come una variabile membro o un nome di un parametro) in un particolare scope (come in una classe interna o nella definizione di un metodo) ha lo stesso nome di un'altra dichiarazione di variabile in uno scope più esterno, allora la dichiarazione nello scope più interno nasconde quello nello scope più esterno.


### Local Classes

Le classi locali sono classi definite in un _blocco_, il quale è un gruppo di zero o più statements tra parentesi graffe bilanciate. Tipicamente troviamo classi locali definite nel corpo di un metodo.

#### Declaring Local Classes

È possibile definire una classe locale all'interno di qualsiasi blocco:

```java
public calss MyClass {
  public void method() {
    //statements
    ...
    class LocalClass {
      // members
    }
  }
}
```

#### Accessing Members of an Enclosing Class

Una classe locale ha accesso ai membri della classe che la contiene. In più una classe locale ha accesso alle variabili locali del blocco in cui è definita.

Tuttavia una classe locale può accedere solamente a variabili locali dichiarate `final`. Quando una classe locale accede ad un variabile o parametro nel blocco in cui è contenuta la classe, _cattura_ quella variabile o parametro.

> **nota:** la variabile _catturata_ viene detta **captured variable**

Da Java 8 una classe locale può accedere a variabili locali e parametri del blocco in cui è definita che sono `final` o `effective final`. Una variabile o parametro il cui valore non è mai cambiato dopo la sua inizializzazione si dice `effective final`. Inoltre, sempre a partire da Java 8, se si dichiara una classe locale in un metodo, la classe può accedere i parametri del metodo.

**Shadowing and Local Classes**

Dichiarazioni di un tipo (per es. una variabile) in una classe locale nasconde dichiarazioni di tipi con stesso nome dello scope più esterno.

#### Local Classe Are Similar To Inner Classes

* Le classi locali sono simili alle classi interne in quanto non possono definire o dichiarare alcun membro _statico_, a meno che non siano costanti, cioè `static final`.

* Una classe locale definita in un metodo statico puo solo riferirisi a membri statici della classe che la contiene.

* Una classe locale non è statica perchè ha accesso ai membri di istanza del blocco in cui è contenuta.

* Non è possibile dichiarare un interfaccia all'interno di un blocco. Le interfacce sono inerentemente statiche.

* Non è possibile dichiarare inizializzatori statici o interfacce mebro in una classe locale. Una classe locale può avere membri statici purchè siano definiti costanti.


### Anonymous Classes

 Le classi anonime consentono di scrivere codice più conciso. Permettono di dichiarare ed instanziare un classe allo stesso tempo. Sono come classi locali ma senza nome. Vengono usate quando si vuole usare una classe locale una sola volta.

#### Declaring Anonymous Classes

Mentre le classi locali sono dichiarazioni di classe, le classi anonime sono espressioni, il che significa che si definisce la classe in un'altra espressione.

#### Syntax Of Anonymous Classes

La sintassi di un'espressione di classe anonima è come un invocazione di un costruttore, tranne per il fatto che esiste una definizione di classe contenuto in un blocco di codice:

```java
MyClass class = new MyClass() {
  // members
};
```

L'espressione di classe anonima consiste:

* L'operatore `new`
* Il nome di un interfaccia da implementare o di una classe da estendere.
* Parentesi che contegono gli argomenti di un costruttore, proprio come una normale espressione di creazione di istanze di classe.
* Un corpo, che è il corpo di dichiarazione della classe.
* In quanto espressione, una classe anonime deve essere parte di uno statement. Quindi, come per ogni altro statement si usa il `;` dopo la chiusura delle parenti graffe

#### Accessing Local Variables of the Enclosing Scope, and Declaring and Accessing Members of the Anonymous Class

Come per le classi locali, le classi anonime possono _catturare variabili_. Hanno lo stesso accesso alle variabili locali dello scope in cui sono racchiuse:

* una classe anonima ha accesso ai membri della classe che la contiene
* una classe anonima non può accedere a variabili locali nello scope in cui è contenuta che non sono dichiarate `final` o effective final
* Come per una classe interna, una dichiarazione di un tipo (come una variabile membro o un nome di un parametro) in un particolare scope (come in una classe interna o nella definizione di un metodo) ha lo stesso nome di un'altra dichiarazione di variabile in uno scope più esterno, allora la dichiarazione nello scope più interno nasconde quello nello scope più esterno

Le classi anonime hanno anche le stesse restrizioni delle classi locali rispetto ai loro membri:

* non si possono dichiarare inizializzatori statici o interfacce membro in una classe anonima
* una classe anonima può avere membri statici purchè siano variabile costanti.

In una classe anonima puoi dichiarare i seguenti:

* Campi
* Metodi aggiuntivi (anche se non possono implementare alcun metodo di un supertipo)
* Inizializzatori di istanziare
* Classi locali

Tuttavia, non è possibile dichiarare costruttori in una classe anonima. Le classi anonime sono ideali per implementare interfacce.

### Lambda Expressions

Un problema con le calssi anonime è che se l'implementazione è semplice, l asintassi può sembrare poco pratica e poco chiara.
Le espressioni lambda consentono di esprimere le istanze delle _calssi a metodo singolo_ in modo più compatto.

> **note:** Un interfaccia funzionale è una qualsiasi interfaccia che contiene solo un metodo astratto.
Siccome contiene solo un metodo si può omettere il nome del metodo quando lo si implementa. Per fare ciò, invece di usare una classe anonima, usiamo un _lambda expression_. Sintassi:

```java
() -> {
  // body's method
}
};
```

### Method References

Si usano espressioni lambda per creare metodi anonimi. A volte, un'espressione lambda non fa altro che chiamare un metodo esistente. In questi caso è più chiaro fare riferimento al metodo esistente per nome. I method reference (reiferimenti a metodo) consentono di farlo. Sono espressioni lambda compatte e facili da leggere per metodi che hanno già un nome.

Il method reference `MyClass::fun` è semanticamente lo stesso dell'espressione lambda `(a.b) -> MyClass.fun(a,b)`. Ognuni ha le seguenti caratteristiche:

* lista dei parametri formali copiata da da quelli del metodo fun, in questo caso a e b
* il corpo chiama il metodo fun

#### Kinds of Method References

Tipologia     | Esempi
--------------|---------
Riferimento a metodo statico      | ContainingClass::staticMethodName
Riferimento ad unmetodo di istanza di un particolare oggetto     | ContainingObject::instanceMethodName
Riferimento ad un metodo di istanza di un particolare metodo di un tipo particolare        | ContainingType::methodName
Riferimento ad un costruttore       | ClassName::new


### When to Use Nested Classes, Local Classes, Anonymous Classes, and Lambda Expressions

* **Classi Locali**: usate se c'è bisogno di creare più di un'istanza di una classe, accedere al suoi construttore.

* **Classi anonime**: usate se c'è bisogno di dichiarare campi o metodi aggiuntivi

* **Espressioni lambda**:
  * usate se si vuole incapsulare una singola unità di comportamento che si vuole passare ad un altro codice
  * usate se si ha bisogno di una semplice istanza di un'interfaccia funzionale e nessuno dei criteri punti si applica

* **Class nidificate**: usate qualore i requisiti sono simili a quelli di una classe locale e si vuole rendere il tipo più disponibile e non si ha bisogno di accedere alle variabili locali o ai parametri di tipo.

  * Utilizzare un classe nidificate non statica (classe interna) se è necessario accedere ai campi dati e ai metodi non pubblici della classe esterna
  * Utilizzare una classe nidificata statica se non si richiede questo accesso


### Enum types

Enum è un tipo di dato che consente ad una variabile di essere un insieme di costanti predefinite. La variabile deve essere uguale a uno dei valori che sono stati predefinit per essa. Poichè sono costanti, i nomi dei campi di un tipo enum sono in lettere maiuscole (segue sintassi delle costanti).

```java
public enum Day {
  LUNEDÌ, MARTEDÌ, MERCOLEDÌ, GIOVEDÌ, VENERDÌ, SABATO, DOMENICA
}
```

Si dovrebbe usare un `enum` ogni volta che c'è l'esigenza di rappresentare un set fisso di costanti e l'insieme di dati di cui si conoscono tutti i valori possibili a tempo di compilazione.

La dichiarazione enum definisce una classe (chiamata tipo enum). Il corpo della classe può includere metodi e altri campi. Il compilatore aggiunge automaticamente alcuni metodi speciali quando crea un `enum`. Per esempio, un metodo di valori statici che resituisce un array contenente tutti i valori dell'enumerazione in ordine di dichiarazione. Si usa per es. per ciclare:

```java
for (Day d : Day.values()) {
  System.out.printl(p);
}
```

> **nota**: Tutti gli `enum` implicitamente estendo `java.lang.enum`. Siccome una classe può estendere solo un 'altra classe, java non supporta l'ereditarietà multipla di stato; di conseguenza un `enum` non può estendere nient'altro.

Nel tipo enum, se definisco metodi e campi dati, le costanti devono essere dichiarate prima di qualsiasi altro campo o metodo e richiedono un `;` alla fine della lista. Il costruttore deve avere modificatore `private` o di package. Il costruttore crea automaticamente le costanti definiti all'inizio del corpo della classe. NOn è possibile invocare il costruttore esplicitamente:

```java
public enum Day
  LUNEDÌ (info a),
  MARTEDÌ (info b); // remember ;

  Day(info i) {
    // code
  }
```

## Annotations

  Le annotazioni forniscono dati su un programma. Hanno numerosi usi:

  * Informazioni per il compilatore: possono essere utilizzate dal compilatore per rilevare errori o sopprimere avvertimenti
  * Elaborazioni a compile time e a deployment time: gli strumenti software possono elaborare informazioni di annotazione per generare codice, file XML ecc.
  * Elaborazione runtime: alcune annotazioni sono disponibili per essere esaminate in fase di runtime

## Interface and inheritance

### Interface

In Java un'interfaccia è un tipo di riferimento, simile ad una classe, che può contenere solo:

* Costanti
* Firme del metodo
* Metodi di default
* Metodi statici
* Tipi nidificati

I corpi dei metodi esistono sono per i metodi di default per i metodi statici
Le interfacce non possono essere istanziate, possono solo essere implementate da classi oppure estese da altre interfacce.

```java
public Interface MyInterface extends Interface1, Interface2, ... {

  //constant declaration
  public static final CONSTANT = value;

  // method signature
  public void method();

  ...

}
```

Per usare un interfaccia bisogna scrivere una classe che implementi tale interfaccia. Quando istanziamo una classe che implementa un interfaccia bisogna fornire un corpo per ciascuno metodo dichiarato.
Il livello di accesso come per le classi è `public` o di package.
Un interfaccia può estendere altre interfacce, proprio come una sottoclasse estende un classe parent. Tuttavia, mentre una classe può estendere solo un'altra classe, un'interfaccia può estendere qualsiasi numero di interfacce.

Il corpo dell'interfaccia può contenere:
* metodi astratti
* metodi di Default
* metodi statici

Tutti i metodi astratti, di default e statici sono implicitamente `public` e si può omettere.

Inoltre può contenere dichiarazioni di costanti. Tutti i valori costanti in una interfaccia sono implicitamente `public`, `static` e `final`. si possono omettere.

#### Implementing an Interface

```java
public class MyClass extends AnotherClass implements Interface1, Interface2, ... {
  ...
}
```

Per convenzione, quando implemento un interfaccia e devo anche derivare da un'altra classe, prima uso `extends` e poi `implements`.

#### Using an Interface as a Type

Quando si definisce una nuova interfaccia si definisce un nuovo tipo. È possibile usare i nome delle interfacce ovunque sia possibile usare qualsiasi altro nome di tipo di dato. Se si definisce una variabile riferimento il cui tipo è un interfaccia, qualsiasi oggetto che gli venga assegnato deve essere un'istanza di una classe che implementa l'interfaccia.

#### Evolving Interfaces

Quando si desidera aggiungere funzionalità ad un interfacci (metodi), conviene creare nuove interfacce che la estendono con le nuopve funzionalità o in alternativa aggiungere metodi di default o nuovi metodi statici.

> **nota**: I metodi di default consentono di aggiungere nuove funzionalità alle interfacce delle librerie e garantire la compatibilità binaria con il codice scritto per le versioni precedenti di tali interfacce.




### Inheritance

Ad eccezione della classe Object, che non ha una superclasse, ogni classe ha una sola superclasse diretta (ereditarietà singola). In assenza di qualsiasi altra superclasse esplicita, ogni classe è implicitamente una sottoclasse di Object.

Le classi possono essere derivate da classi derivate da classi derivate da classi e così via e, infine, derivate dalla classe più in alto, Object. Si dice che tale classe discenda da tutte le classi nella catena dell'eredità che si estende da Object.

L'idea di ereditarietà è semplice ma potente: quando vuoi creare una nuova classe e c'è già una classe che include parte del codice che desideri, puoi ricavare la tua nuova classe dalla classe esistente. Nel fare questo, puoi riutilizzare i campi e i metodi della classe esistente senza doverli scrivere.

Una sottoclasse eredita tutti i membri (campi, metodi e classi nidificate) dalla sua superclasse. I costruttori non sono membri, quindi non sono ereditati da sottoclassi, ma il costruttore della superclasse può essere invocato dalla sottoclasse.


#### What You Can Do in a Subclass

Una sottoclasse eredita tutti i membri pubblici e protetti della sua classe padre, indipendentemente dal package in cui si trova la sottoclasse. Se la sottoclasse si trova nello stesso package della classe padre eredita anche i suoi membri con accesso package. Puoi utilizzare i membri ereditati così come sono, sostituirli, nasconderli o completarli con nuovi membri:
* I campi ereditati possono essere utilizzati direttamente, proprio come qualsiasi altro campo.
* E' possibile dichiarare un campo nella sottoclasse con lo stesso nome di quello nella superclasse (non consigliato), nascondendolo.
* Si possono creare nuovi campi dati nella sotoclasse che non sono presenti nella superclasse
* I metodi ereditati possono essere utilizzati direttamente così come sono
* si può scrivere un nuovo metodo di istanza nella sottoclasse che ha la stessa firma di quella nella superclasse, quindi fare un override.
* Si può scrivere un nuov metodo statico nella sottoclasse che ha la stessa firma di quello nella superclasse, quindi fare un override.
* Si possono dichiarare nuovi metodi nella sottoclasse che non superclasse
* Si può scrivere un costruttore della sottoclasse che richiama il costruttore della superclasse, implicitamente o usando la keyword `super`.

#### Private Member in a Superclass

Una sottoclasse non eredita i membri `private` della sua superclasse diretta. Tuttavia, se la superclasse ha metodi marcati `public` o `protected` che accedono ai suoi campi privati, questi possono essere usati dalla sottoclasse.

Una classe nidificata ha accesso a tutti i membri privati della classe che la contiene, sia campi dati che metodi. Perciò una classe nidificate marcata `public` o `protected` ereditata da una sottoclasse ha accesso indiretto a tutti i membri privati della superclasse.

#### Casting Objects

Il casting mostra l'uso di un oggetto di un tipo al posto di un altro tipo, tra gli oggertti consentiti dall'ereditarietà e dalle implementazioni.

> **nota**: è possibile eseguire un test logico sul tipo di un particolare oggetto utilizzando l'operatore `instanceof`. Può salvarti da un errore di runtime a causa di un cast improprio.

#### Multiple Inheritance of State, Implementation, and Type

L'ereditarietà multipla di implementazione è la capacità di ereditare definizioni di metodi da più classi. Possono sorgere conflitti in questo tipo di ereditarietà (di nome, ambiguità). I metodi di default introducono una forma di eredità multipla di implementazione. Una classe può implementare più di un'interfaccia, che può contenere metodi di default con lo stesso nome. Il compilatore fornisce alcune regole per determinare quale metodo di default utilizza una determinata classe.

L'ereditarietà multipla di tipo è la capacità di una classe di implementare più di un'interfaccia. Un oggetto può avere più tipi: il tipo della sua classe e i tipi di tutti le interfacce implementate dalla classe. Ciò significa che se una variabile viene dichiarata di tipo Interfaccia, allora il suo valore può riferire qualunque oggetto che è istanziato da qualsiasi classe che implementa quell'interfaccia.

Una classe può ereditare diverse implementazioni di un metodo definito (default o statico) nelle interfacce che estende. In questo caso, il compilatore o l'utente deve decidere quale utilizzare.


#### Overriding and Hiding Methods

##### Instance Methods

Un metodo di istanza in una sottoclasse con:

* stessa firma (nome, numero e tipo di parametri)
* stesso tipo di ritorno o covariante

sovrascrive il metodo della superclasse (override).

L'abilità di una sottoclasse di fare un override di un metodo permette di ereditare tale metodo da una superclasse il cui comportamento è abbastanza vicino e quindi di modificarne il comportamento secondo necessità. L'override ha stesso nome, numero di parametri e tipo di ritorno del metodo che viene sovrascritto. Un metodo sovrascritto può anche essere ritornare un sottotipo del tipo redtituito dal metodo sottoposto ad override. Questo sottotipo è chiamato tipo di ritorno covariante.

Quando si fa override di un metodo, è possibile usare l'annotazione @Override che indica al compilatore che si intende sovrascrivere un metodo nella superclasse.


##### Static Method

Se una sottoclasse definisce un metodo statico con la stessa firma di un metodo statico nella superclasse, il metodo nella sottoclasse nasconde quello nella superclasse.

La distinzione tra nascondere un metodo statico e fare un ovveride di un metodo di istanza ha risvolti importanti:

* La versione del metodo di istanza sottoposto ad override che viene richiamato è quello della sottoclasse.
* La versione del metodo statico nascosto che viene richiamato dipende dal fatto che sia invocato dalla supercalsse o dalla sottoclasse.

##### Interface Methods

Metodi di default e metodi astratti nelle interfacce sono ereditati come metodi di istanza. Tuttavia, quando i supertipi di una classe o di un'interfaccia forniscono più metodi predefiniti con la stessa firma, il compilatore Java segue le regole di ereditarietà per risolvere il conflitto di nomi. Queste regole sono guidate dai seguenti due principi:

* I metodi di istanza sono preferiti rispetto ai metodi di default dell'interfaccia
* I metodi già sovrascritti da altri candidati vengono ignorati. Questa circostanza può sorgere quando i supertipi condividono un antenato comune.

Se una classe implementa due interfaccie identiche, per esempio con un metodo di default identico, si può scegliere quale dei due invocare attraverso la keyword `super`.

Il nome che precede `super` deve fare riferimento ad una superinterfaccia/superclasse diretta che definisce o eredita il metodo. E' possibile usare `super` per invocare un metodo di default sia in classi che in interfacce.

> **nota**: Metodi statici in interfacce non sono mai ereditati

##### Modifiers

Il modificatore d'accesso per un metodo overraidato può "permettere di pù",  ma non meno. Dà un errore di compilazione.

> **nota**: n una sottoclasse, è possibile overloaddare i metodi ereditati dalla superclasse. Tali metodi non nascondono né sovrascrivono i metodi di istanza della superclasse: sono nuovi metodi, unici per la sottoclasse.

#### Hiding Fileds

All'interno di una classe, un campo che ha lo stesso nome di un campo nella superclasse nasconde il campo della superclasse, anche se i loro tipi sono diversi. All'interno della sottoclasse, il campo nella superclasse non può essere referenziato con il suo semplice nome ma può essere acceduto tramite la keytword `super`.
In generale, non è consigliabile nascondere i campi poiché rende il codice difficile da leggere.

#### Using the Keyword `super`

##### Accessing Superclass Members

Se un metodo sovrascrive (overrides) uno dei metodi della sua superclasse, si può invocare il metodo sovrascritto tramite l'uso dell keyword `super`. Si può usare anche per fare riferimeto ad un campo nascosto (meglio non nascondere mai i campi).

##### Subclass Constructors

La sintassi per chiamare un costruttore di una superclasse è:
```java
super();

// or

super(parameter list)
```

Con `super()` viene chiamato il costruttore senza argomenti dell superclasse. Con `super(parameter list)` viene chiamato il costruttore della superclasse cun una lista di parametri corrispondente.

> **nota**: se un costruttore nella sottoclasse non richiama esplicitamente un costruttore nella superclasse, il compilatore Java inserisce automaticamente una chiamata al costruttorre senza argomenti della superclasse. Se la superclasse non ha un costruttore senza argomenti(per es. perchè ne è stato definito uno esplicitamente con uno o più parametri), allora si otterà un errore in fase di compilazione.

Se un costruttore di una sottoclasse richiama un costruttore della sua superclasse, in modo esplicito o implicito, si potrebbe pensare che venga chiamata un'intera catena di costruttori , fino al costruttore di Object. In effetti, è proprio così. Si chiama _constructor chaining_.

#### Objects as a Superclass

La classe Object, situata nel package `java.lang`, si trova nella parte più alta della gerarchia delle classi. Ogni classe discende direttamente o indirettamente da Objcet ed eredita i metodi di istanza da Object. Non è necessario utilizzare nessuno di questi metodi, ma, se si sceglie di farlo, si potrebbe avere la necessità sostituirli con codice specifico per la classe. Alcuni dei metodi ereditati da Object sono:

* `protected Object clone() throws CloneNotSupportedException`: crea e ritorna una copia di questo oggetto
* `public boolean equals(Object obj)`: indica se altrioggetti sono uguali a questo
* `protected void finalize() throws Throwable`: Chiamato dal garbage collector su di un oggetto quando il garbage collector determina che non ci sono più riferiementi a quell'oggetto.
* `public final Class getClass()`: ritoena la classe a runtime de un oggetto
* `public int hashCode()`: ritorna l'hashcode di un oggetto
* `public String toString()`: ritorna una rappresentazione in forma di stringa di un oggetto

##### The `clone()` Method

Se una classe o una delle sue superclassi, implementa l'interfaccia `Cloneable`, si può usare il metodo `clone()` per creare una copia da un oggetto esistente.

```java
aCloneableObject.clone();
```
L'implementazione di questo metodo controlla se l'oggetto su cui è stato invocato `clone()` implementa l'interfaccia `Cloneable`. Se l'oggetto non lo fa, il metodo lancia un'eccezione `CloneNotSupportedException`. Se si sta per scrivere un  metodo `clone()` sovrascrivendolo dalla classe Object, può essere dichiarato come:

```java
protected Object clone() throws CloneNotSupportedException
    /// or
public Object clone() throws CloneNotSupportedException
```

Se l'oggetto su cui è stato invocato `clone()` implementa l'interfaccia Cloneable, l'implementazione dell'oggetto del metodo `clone()` crea un oggetto della stessa classe dell'oggetto originale e inizializza le variabili membro del nuovo oggetto con gli stessi valori dell'oggetto originale.

Per alcune classi, il comportamento predefinito del metodo `clone()` ereditato da Object funziona perfettamente. Tuttavia se un oggetto contiene un riferimento a un oggetto esterno, potrebbe essere necessario eseguire l'override del metodo `clone()` per ottenere un comportamento corretto.


##### The `equals()` Method

Il metodo`equals()` confronta 2 oggetti e ne verifica l'uguaglianza. Restituisce true se sono uguali. Il metodo `equals()` fornito dalla classe Object utilizza l'operatore id identità `==` per determinare se due oggetti sono uguali. Per i tipi primitivi, questo fornisce il risultato corretto. Per gli oggetti non è così, infatti verifica se i riferimenti sono uguali, ovvero se gli oggetti confrontati sono esattamente lo stesso oggetto. Per verificare se due oggetti sono uguali nel senso di equivalenza (ossia contengono la stessa informazione), è necessario fare un override del metodo `equals()`.

> **nota**: se si fa un override del metodo `equals()` si deve anche fare l'ovveride del metodo `hasCode()`.

##### The `getClass()` method

Non è possibile fare override di questo metodo. Il metodo `getClass()` restituisce un oggett di tipo `Class`, cha ha metodi che è possibile utilizzare per ottenere informazioni sulla classe, come il suo nome, la sua superclasse e le interfacce implementate.

##### The `hashCode` method

Il valore restituito da questo metodo è l'hash dell'oggetto, che è l'indirizzo di memoria dell'oggetto in esadecimale.
Per definizione, se due oggetti sono uguali, anche il loro codice hash deve essere uguale. Se si esegue l'override del metodo `equals()` si modifica il modo in cui i due oggetti sono equivalenti e l'implementazione di `hashCode()` dell'oggetto non è più valida. Pertanto se si esegue l'override del metodo `equals()`, è necessario anche sovrascrivere il metodo `hashCode()`.


##### The `toString()` Method

Dovresti sempre considerare di sovrascrivere il metodo toString () nelle tue classi.

Il metodo `toString()` dell'oggetto restituisce una rappresentazione in formato `String` dell'oggetto. La rappresentazione dipende interamente dall'oggetto, motivo per cui è necessario eseguire l'override di `toString()` nelle classi.


#### Writing Final Classes and Methods

Si possono dichiarare alcune o anche tutti i metodi di una classe `final`. Si usa la keyword `final` nella dichiarazione di un metodo che non potrà essere overraidato da una sua sottoclasse. S potrebbe bensare di rendere un metodo `final` se è implementato in modo tale che un override renda incoerente la classe.


#### Abstract Method and Classes

Una classe astratta è una classe che è dichiarata `abstract` (può includere o meno metodi astratti). Una classe astratta non
può essere istanziata, ma può essere estesa da una sottoclasse.

Un metodo astratto è un metodo dichiarato senza un'implementazione come questo:

```java
abstract void abstractMethod(double x, double y);
```

Se una classe contiene almeno un metodo astratto **deve** essere dichiarata astratta.
Quando una classe astratta viene estesa da una sua sottclasse, la sottoclasse solitamente fornisce un'implementazione per tutti i metodi astratti. Tuttavia, se non lo fa, allora anche la sottoclasse deve essere dichiarata astratta.

> **nota**: I metodi nelle interfacce che non sono statici o di default sono implicitamente astratti, quindi non è necessario usare la keyword `abstract`.

##### Abstract Classes Compared to Interfaces

Le classi astratte sono simili alle interfacce. Non è possibile istanziarle e possono contenere un mix di metodi con o senza un'implementazione. Tuttavia, con le classi astratte, è possibile dichiarare:
* campi non statici e `final`
* definire metodi concreti marcati `public`, `protected` o `private`.

Nelle interfacce, tutti i campi sono automaticamente `public`, `static` e `final` e tutti i metodi che dichiari o definisci (come metodi di default o statici) sono `public`. Inoltre, è possibile estendere solo una classe, indipendentemente dal fatto che sia astratta, mentre è possibile implementare un qualsiasi numero di interfacce.

E' consigliato usare una classe astratta quando una di queste affermazioni si applica alla situazione:

*  Vuoi condividere il codice tra diverse classi strettamente correlate
*  Ti aspetti che le classi che estendono la tua classe astratta abbiano molti metodi o campi comuni o richiedano modificatori di accesso diversi da `public`
*  Si desidera dichiarare campi non statici o non `final`. Ciò permette di dichiarare metodi che possono accedere e modificare lo stato corrente dell'oggetto a cui appartengono.

una classe astratta quando una di queste affermazioni si applica alla situazione:

* Ti aspetti che classi non correlate implementino la tua interfaccia. Per esempio le interfacce Comparable e Cloneable sono implementate da molte classi non correlate
* Si desidera specificare il comportamento di un particolare tipo di dati, ma non ci si preoccupa di chi implementa il suo comportamento.
* Si vuole sfruttare l'ereditarità multipla di tipo


##### When an Abstract Class implements an Interface

Una classe che implementa un'interfaccia deve implementare tutti i suoi metodi per poter essere istanziata. Tuttavia, è possibile definire una classe che non implementa tutti i metodi dell'interfaccia, a condizione che la classe sia dichiarata astratta.

##### Class Members

Una classe astratta può avere campi statici e metodi statici. Si possono usare questi membri statici con un riferimento ad una classe come per qualsiasi altra classe non astratta.



## Number and Strings

### Numbers

#### The Number Classes

<p align="center">
  <img src="/img/Number.png" width="350"/>
</p>
</br>

Ci sono ragioni per cui è meglio usare oggetti Number invece che primitivi. La piattaforma Java offre classi `Wrapper` per ogni primitivo. Queste classi wrappano i primitivi in oggetti. Spesso il wrapping è effettuato dal compilatore:
se si usa un tipo primtivo quando è atteso un oggetto, il compilatore `boxes` il primitivo nella sua classe wrapper automaticamente. Se invece si usa un oggetto quando è atteso un primitivo, il compilatore `unboxes` l'oggetto automaticamente.

Ci sono **3** ragioni per cui si dovrebbe usare un Oggetto number invece di un primitivo:

* Come argomento di un metodo che si aspetta un oggetto (spesso quando simanipola una collezione di numeri)

* Per usare costanti definite da una classe, come per esempio `MIN_VALUE` e `MAX_VALUE`, che forniscono il limite inferiore e superiore del tipo di dato.

* Per usare metodi di classe per convertire valori a/da altri tipi primitivi, per convertire a/da `String`, e per convertire tra sistemi numerici (decimale, ottale, esadecimale, binario)

>**nota**: Tutte le sottoclassi di Number implementano il metodo `equals`. Due Number sono uguali se hanno stesso tipo  stesso valore numerico.



### Character

Ci sono volte in cui è necessario utilizzare un `char` come oggetto, ad esempio come argomento del metodo in cui è previsto un oggetto. Il linguaggio di programmazione Java fornisce una classe wrapper che "avvolge" il carattere in un oggetto `Character` per questo scopo. Un oggetto di tipo `Character` contiene un singolo campo, il cui tipo è char. Questa classe di caratteri offre anche una serie di metodi di classe utili (cioè, statici) per manipolare i caratteri.

Il compilatore Java può creare automaticamente, come nel caso di Number, un oggetto `Character` in alcune circostanze. Ad esempio, se si passa un carattere primitivo in un metodo che si aspetta un oggetto, il compilatore converte automaticamente il chare in un `Character`. Questa funzione è chiamata autoboxing o unboxing, se la conversione va nella direzione opposta.

>**nota**: La classe CHaracter è immutabile; una volta creato, un `Character` non può essere cambiato.

#### Escape Sequences

Un `char` precduto da un backslash `\` è una sequenza di escape e ha un significato speciale per il compilatore.

Escape Sequence|Descrizione
---------------|-----------
`\t`  | inserisce un tab
`\b`  | inserisce uno spazio
`\n`  | inserisce una nuova linea
`\f`  | inserisce un formfeed
`\'`  | inserisce a single quote
`\"`  | inserisce a double quote
`\\`  | inserisce un backslash



### Strings

`Strings` sono sequenze di caratteri. In Java sono oggetti.

```java
String greeting = "Hello Wrold!";
```
In questo caso `Hello World!` è un litterale stringa (una serie di caratteri nel codice racchiusa tra doppi apici) Tutte le volte in cui si incontra un litterale stringa nel codice, il compilatore crea un oggetto Stringa con il suo valore (in questo caso `Hello World`).

Come qualsiasi altro oggetto, si può creare oggetti `String` tramite `new` e un costruttore.

>**nota**: La classe `String` è immutabile. Una volta creato un oggetto di tipo `String` non può essere modificato. La classe `String` contiene numerosi metodi che sembrano modificare la stringa di partenza. Tuttavia questi metodi in realtà creano un nuovo oggetto stringa a partire dal precedente.



### Autoboxing and Unboxing

**Autoboxing** è la conversione automatica che il compilatore fa tra tipi primitivi ed i corrispondenti oggetti della classe wrapper.

Il compilatore Java applica l'autoboxing quando un primitivo è:
* passato come parametro ad un metodo che si aspetta un oggetto della corrispondente classe wrapper
* assegnato ad una variabile della corrispondente classe wrapper

L' **Unboxing** è la conversione di un oggetto di un tipo wrapper al suo corrispondente tipo primitivo.
Il compilatore Java applica l'unboxing quando un oggetto wrapper è:
* passato come parametro ad un metodo che si aspetta un valore del corrispondente tipo primitivo
* assegnato ad una variabile del corrispondente tipo primitivo


## Generics

### Why Use Generics?

I generici consentono ai tipi di essere parametrizzati quando definiamo classi, interfacce e metodi. I parametri di tipo forniscono un modo per riusare lo stesso codice con differenti input. La differenza è che gli inpuit dei parametri formali sono valori, mentre gli input dei parametri di tipo so tipi.
Il codice che utilizza i generics ha molti vantaggi rispetto al codice non-generics:

* Controlli di tipo più potenti a tempo di compilazione: il compilatore Java applica un forte controllo di tipo al codice generico e genera errori se il codice viola la sicurezza del tipo. Correggere gli errori in fase di compilazione è più semplice che correggere errori a runtime

* Eliminazione di cast:

```java
List list = new ArrayList();
list.add("Hello");
String s = (String) list.get(0);

List<String> list = new ArrayList<String>();
list.add("Hello");
String s = list.get(0); // no cast
```
* Abilitano i programmatori ad implementare algoritmi generici


### Generics Types

Un tipo generico è un classe generica o interfaccia parametrizzata sui tipi.
Una _classe generica_ è definita nella seguente forma:

```java
class name<T1, T2, ..., Tn> {/* ... */}
```

Un parametro di tipo può essere qualsiasi tipo **non primitivo**: qualsiasi classe, qualsiasi interfaccia, qualsiasi array. La stessa tecnica è usata per creare interfacce generiche.


### Type Parameter Naming Convention

Per convenzione, i parametri di tipo sono lettere singole maiuscole. Le elettere più usate sono:

* E - Element
* K - Key
* N - Number
* T - Type
* V - Value
* S, U, V etc. - 2nd, 3rd, 4th types


### Invoking and Instantiating a Generic Type

```java
Class<Integer> integerClass;
```

In questo modo **dichiariamo** un riferimento ad una classe generica istanziata con Integer (è il type argument).

>**nota**: `T` in `MyClass<T>` è un type parameter (parametro di tipo) mentre `Integer` in `MyClass<Integer> i` è un type argument (argomento di tipo).

Per **istanziare** una classe generica, usiamo come sempre la keyword `new` con il type argument come nella dichiarazione.

```java
Class<Integer> integerClass = new Class<Integer>();
```

### The Diamond

Con Java SE 7 è possibile sostituire gli argomenti di tipo richiesti per invocare il costruttore di una classe generica con un set vuoto di argomenti di tipo a condizione che il compilatore possa determinare o dedurre (infer) gli argomenti di tipo dal contesto (solitamente dalla dichiarazione).

```java
Class<Integer> integerClass = new Class<>();
```


### Raw Types

Un **raw type** è il nome di una classe o interfaccia generica senza alcun argomento di tipo.

```java
public class MyClass<T> { /* ... */}
MyClass class = new MyClass(); // raw type
```

In questo caso `MyClass` è un raw type del tipo generico `MyClass<T>`. Tuttavia una classe o interfaccia non generica **non** è un raw type.


#### Unchecked Error Messages

Il termine **Unchecked** significa che il compilatore non ha abbastanza informazioni per fare tutti i check di tipo necessari per assicurare la sicurezza sui tipi. Per vedere tutti i warning unchecked, ricompilare con `-Xlint:unchecked`.


### Generic Methods

Metodi generici sono metodi che introducono i loro propri parametri di tipo. È simile alla dichiarazione di un tipo generico, ma lo scope del parametro di tipo è limitato a quello del metodo. I parametri di tipo sono permessi sia a metodi statici che non statici, e anche a costruttori di classi generiche.

La sintassi per un metodo generico include una lista di parametri di tipo, all'interno di parentesi angolari, la quale appare prima del metodo di ritorno del tipo. Per metodi generici statici, la sezione dei parametri di tipo **deve** apparire prima del tipo di ritorno del metodo.

```java
public class MyClass{
    public static <K, V> boolean compare(Pair<K, V> p1, Pair<K, V> p2) {
        return p1.getKey().equals(p2.getKey()) &&
               p1.getValue().equals(p2.getValue());
    }
}
```



### Bounded Type Parameters

Ci sono situazioni in cui si vogliono restringere i tipi che possono essere usati come argomenti di tipo in un tipo parametrizzato. Questo è cioè che un parametro di tipo fa.

Per dichiarare un parametro di tipo limitato si scrive il nome del parametro di tipo seguito dalla parola chiave `extends` seguita dal suo limite superiore (upper bound).

```java
public class MyClass<T extends Number> { /* ... */}
```


#### Multiple Bounds

Un parametro di tipo può avere bounds multipli:

```java
public class MyClass<T extends A & B2 & B3> { /* ... */}

class A { /* ... */ }
interface B { /* ... */ }
interface C { /* ... */ }
```

Una variabile di tipo T con bound multipli è un sottotipo di tutti i tipi presenti nella lista. Se uno di questi è una classe, deve essere specificata per prima.



### Generics, Inheritance and Subtypes


<p align="center">
  <img src="/img/generics-subtypeRelationship.gif" width="350"/>
</p>
</br>

`Box<Integer>` e `Box<Double>` non sono sottotipi di `Box<Numeber>`.

### Type Inference

La type inference è la capacità del compilatore Java di guardare ogni invocazione di metodo e relativa dichiarazione per determinare l'argomento di tipo che rende l'invocazione applicabile.
L'algortmo di deduzione determina i tipi degli argomenti e, se disponibile, il tipo al quale viene assegnato o restituito il risultato. Infine, l'algoritmo cerca di trovare il tipo più specifico che funzioni con tutti gli argomenti.

#### Type Inference and Generic Methods
I metodi generici ci introducono alla type inference, la quale abilita all'invocazione di un metodo generico come se fosse un metodo ordinario, senza specificare un tipo tra parentesi angolari.
Per esempio:

```java
public static <U> void addBox(U u, List<Box<U>> boxes) {
    Box<U> box = new Box<>();
    box.set(u);
    boxes.add(box);
  }

  ...

  BoxDemo.<Integer>addBox(Integer.valueOf(10), listOfIntegerBoxes); // specificato parametro con un type witness
  BoxDemo.addBox(Integer.valueOf(20), listOfIntegerBoxes); // omesso il type witness
```

Il metodo geenerico `addBox` definisce un parametro di tipo `U`. Generalmente il compilatore JAva può dedurre i parametri di tipo di una chiamata ad un metodo generico. Conseguentemente, nella maggior parte dei casi, non serve specificare il parametro di tipo (restituito in questo caso).


#### Type inference and Instantiation of Generic Classes
Si può replicare l'argomento di tipo richiesto per invocare il costruttore di una classe generica con un le parentesi angolari vuote. Il compilatore dedurra l'argomento di tipo dal contesto.

```java
Map<String, List<String>> myMap = new HashMap<String, List<String>>();

// questa dichiarazione è sostituibile con:

Map<String, List<String>> myMap = new HasMap<>();
```
Se non si usano le parentesi angolari vuote, il compilatore genera un warning per converisione non verificata (unchecked conversion) in quanto il costruttore `HasMap()` si riferisce al __raw type__ `HasMap` e non a `Map<String, List<String>>`.

#### Type Inference and Generic Constructors of Generic and Non-Generic Classes

Nota che i metodi costruttori possono essere generci sia nelle classi generiche che in quelle non generiche.

```java
class MyClass<X> {
  <T> MyClass(T t) {
    // ...
  }
}

new MyClass<Integer>("");
```

L'ultimo statement crea un istanza del tipo parametrizzato `MyClass<Integer>`. Lo statement specifica esplicitamente il tipo `Integer` per il paramatro formale di tipo `X`, della classe generica `MyClass<X>`. Il costruttore per questa classe generica contiene un parametro formale di tipo `T`. Il compilatore deduce il tipo `String` per il parametro formale `T` del costruttore di questa classe generica perchè il parametro attuale di questo costruttore è di tipo String.

I compilatori prima di Java SE 7 erano in grado di dedurre il tipo dei parametri attuali di costruttori generici, in maniera simile ai metodi generici. Tuttavia, i compilatori da Java SE 7 in poi possono dedurre i parametri di tipo attuali della classe generica che viene istanziata solo se si usano le parentesi angolari vuote `<>`.

```java
MyClass<Integer> myObj = new MyClass<>("");
```

In questo esempio il compilatore deduce il tipo `Integer` per il parametro di tipo `X` della classe generica `MyClass<X>`. Inoltre deduce il tipo `String` per il parametro formale di tipo `T` per il costruttore della classe generica.


#### Target Type
Il compilatore Java sfrutta il tipo target per dedurre i parametri di una invocazione di un metodo generico. Il __tipo target__ di un' espressione è il tipo di dato che il compilatore si aspetta a seconda di dove appare quell'espressione.
Per esempio la dichiarazione del metodo `Collections.emptyList();`

```java
static <T> List<T> emptyList();

List<String> listOne = Collections.emptyList();
```

L'ultimo statement si aspetta un'istanza di `List<String>`. `List<String>` è il tipo target. Poichè il metodo `emptyList` ritorna un valore di tipo `List<T>`, il compilatore deduce che l'argomento di tipo `T` deve essere `String`. Questo meccanismo funziona in Java SE 7 e 8. Alternativamente si può usare un tipo witness e specificare il valore di `T` come nell'esempio qui sotto:

```java
List<Stirng> listOne = Collections.<String>emptyList();
```

Tuttavia non è necessario in questo contesto. E invece necessario in altri contesti. Considera il seguente esempio:

```java
void processListString(List<String> stringList) {
// process stringList
}
```

Si supponga di voler invocare il metodo `process StringList` con una lista vuota. In Java SE 7, il seguente statement non compila:

```java
processStringList(Collections.emptyList());
```

Il compilatore Java SE 7 richiede un valore per l'argomento di tipo `T` e inizia con il tipo `Object`. Successivamente, l'invocazione di `Collections.emptyList` ritorna un valore di tipo `List<Object>` che è incompatibile con con il metodo `processStringList` (tipo di ritorno List<String> incompatibile con List<Object>). Perciò in Java SE 7 si deve specificare il tipo del valore dell'argomento come nell'esempio sotto:

```java
processStringList(Collections.<String>emptyList());
```

Questo non è necessario in Java 8. Il concetto di *"cos'è un tipo target"* è stato esteso includendo gli argomenti di un metodo, come l'argomento del metodo `processStringList`. In questo caso, `processStringList` richiede un argomento di tipo `List<String>`. Il metodo `Collections.emptyList` ritorna un valore di tipo `List<T>` e usando il tipo target di `List<String>`, il compilatore deduce che l'argomento di tipo `T` ha valore di tipo `String`. Perciò in Java 8, il seguente statement compila:

```java
processStringList(Collections.emptyList());
```


### Wildcards

Nel codice generico, il punto di domando `?`, chiamato *wildcard*, rappresenta un tipo sconosciuto. Il wildcard può essere usato in molte situazioni:

* come tipo di un parametro
* campo dati o variabile locale
* come tipo di ritorno

Il wildcard non è mai usato come argomento di tipo per:

* un invocazione di metodo generico
* la creazione di un'istanza di una classe generica
* come supertipo


#### Upper Bounded Wildcards

Si può usare un wildcard limitato superiormente (upper bounded wildcard) per "rilassare" le restrizioni su di una variabile. Per esempio se si vuole usare un metodo che lavori con `List<Integer>`, `List<Double>`, `List<Number>` lo si può fare usando un upper bounded wildcard.

Per dichiarre un upper-bounded wildcard si usa il carattere `?` seguito dalla keyword `extends`, seguita dai suoi bound superiori. Si noti che in questo contesto la keyword `extends` è usata in senso generale e inculde sia `extends` che `implements`.

Per scrivere un metodo che lavori correttamente su liste di `Number` e sottotipi di `Number`, come `Integer`, `Double` e `Float`, si dovrebbe specificare `List<? extends Number>`. Il termine `List<Number>` è più restrittivo perchè matcha solo con una lista di `Number` mentre il `List<? extends Number>` matcha con una lista di `Number` o di una qualsiasi sottoclasse di `Number`.

```java
public static void process(List<? extends Foo> list)
```

Nello statement sopra l'upper bounded wildcard `<? extends Foo>`, dove `Foo` è un tipo qualsiasi, matcha con `Foo` ed un qualsiasi suo sottotipo.

#### Unbounded Wildcards

Il tipo Unbounded wildcards è specificato usando il carattere wildcard `?`, per esempio `List<?>`. Questa è chiamata una *lista di tipo sconosciuto*. Ci sono due scenari nei quali è buona pratica usare un unbounded wildcard:

* Se si sta scrivendo un metodo che può essere implementato usando funzionalità fornite dalla classe `Object`
* Quando il codice utilizza metodi nella classe genrica che **non** dipendono dal parametro di tipo; ad es. `List.size` o `List.clear`. Infatti, `Class<?>` è così spesso usata perchè la maggior parte dei metodi in `Class<T>`non dipende da `T`.

Si consideri l'esempio:

```java
public static void printList(List<Object> list) {
    for (Object elem : list)
        System.out.println(elem + " ");
    System.out.println();
}
```

L'obiettivo di `printList` è quello di stampare una lista di un tipo qualsiasi, ma in questo caso non raggiunge l'obiettivo in quanto stampa solo istanze di `Objects`. Per scrivere un generico metodo `printList` usiamo `List<?>`:


```java
public static void printList(List<?> list) {
    for (Object elem: list)
        System.out.print(elem + " ");
    System.out.println();
}
```

#### Lower Bounded Wildcards

Un lower bounded wildcard restringe il tipo sconosciuto ad essere un tipo specifico o un supertipo di quel tipo.

> **nota:** Non è possibile specificare contemporaneamente un upper bound e un lower bound per un wildcard.

Per dichiarre un lower-bounded wildcard si usa il carattere `?` seguito dalla keyword `super`, seguita dai suoi bound inferiori.

Per esempio se si vuole scrivere un metodo che inserisca oggetti di tipo `Integers` in una lista. Per massimizzarne la flessibilità si vuole che il metodo funzioni su liste di `Integer`, `Number`, `Object`, cioè qualsiasi cosa che possa contenere valori di tipo `Integer`. Il termine `List<Integer>` è più restrittivo di `List<? super Integer>`in quanto il primo matcha con una lista di `Integer` soltanto, mentre il secondo matcha con una lista di un qualsiasi supertipo di `Integer`.


#### Wildcards e Subtyping

Come descritto in Generics, Inheritance e Subtypes, le classi generiche o le interfaccenon sono correlate tra loro semplicemente perchè esiste una relazione tra i loro tipi. Tuttavia è possibile utilizzare i wildcards per creare una relazione tra classi generiche o interfacce.

Date le due classi seguenti:

```java
class A {/* ... */}
class B extends a {/* ... */}
```

E ragionevole scrivere il seguente codice:

```java
B b = new B();
A a = b;
```

L'esempio mostra che l'ereditarietà per classi regolari segue le regole di sottotipaggio: la classe `B` è un sottotipo di `A` se `B` estende `A`. Questa regola **non** è applicabile ai tipi generici:

```java
List<B> lb = new ArrayList<>();
List<A> la = lb; // compile-time error
```

Dato che `Integer` è un sottotipo do `Number` qual'è la possibile relazione tra `List<Integer>` e `List<Number>`

<p align="center">
  <img src="/img/Number.png" width="350"/>
</p>
</br>

Anche se `Integer`è un sottotipo di `Number`, `List<Integer>` non è un sottotipo di `List<Number>` e i due tipi non sono correlati. Il supertipo comune di `List<Number>` e `List<Integer>` è `List<?>`. In modo da creare una relazione tra queste classi e quindi accedere ai metodi di `Number` attraverso elementi di `List<Integer>`, cioè attraverso `Integer`, si usa un upper bound wildcard:

```java
List<? extends Integer> intList = new ArrayList<>();
List<>? extends Number> numList = initList;
```

In quanto `List<? extends Integer>` è un sottotipo di `List<>? extends Number>`

#### Wildcard Capture and Helper Methods

In alcuni casi il compilatore deduce il tipo di un wildcard. Per esempio, una lista può essere definita come `List<?>`, ma quando viene valutata un'espressione, il compilatore deduce un particolare tipo a partire dal codice. Questa situazione si chiama *wildcard capture*.

Solitamente non è c'è da preoccuparsi del wildcard capture, eccetto quando il compilatore produce messaggi che contengano la frase `capture of`. Per esempio:

```java
public class WildcardError {

    void foo(List<?> i) {
        i.set(0, i.get(0));
    }
}

```

In questa situazione il compilatroe processa il parametro `i` come di tipo `Object`. Quando il metodo `foo` invoca `List.set(int, E)`, il compilatore non è in grado di confermare il tipo dell'oggetto che deve essere inserito nella lista e viene prodotto un errore. Quando viene prodotto questo tipo di errore il compilatore crede che si stia assegnando un tipo sbagliato alla variabile. I generici sono stati aggiunti al linguaggio Java proprio per questa ragione, cioè per rafforzare la sicurezza del tipo a compile time.

Nel seguente esempio si dimostra l'uso di un metodo privato helper che serve per risolvere il problema di quando si stanno facendo operazioni sicure ma a causa del wildcard capture viene segnalato un errore.

```java
public class WildcardFixed {

    void foo(List<?> i) {
        fooHelper(i);
    }

    // Helper method created so that the wildcard can be captured
    // through type inference.
    private <T> void fooHelper(List<T> l) {
        l.set(0, l.get(0));
    }

}
```

Grazie ad un metodo helper, il compiltore grazie alla type inference deduce che il tipo da determinare (capture variable) è `T`.

Per convenzione, i metodi helper sono chiamati: `originalMethodNameHelper`.


#### GuideLines for Wildcard Use

Per lo scopo della seguente discussione è utile pensare una variabile come:

* Una variabile "**In**": fornisce dati al codice. Per esempio il seguente metodo di copia con due argomenti: `copy(src, dest)`. L'argomento `src` fornisce i dati che saranno copiati, di conseguenza è il parametro "**In**".
* Una variabile "**Out**": contiene i dati da usare altrove. Nell'esempio di copia l'argomento `dest` accetta i dati ed è il parametro"**Out**".
Naturalmente, alcune variabili vengono utilizzate sia per scopi "In" che "Out"

Si può usare il principio "In" e "Out" qunado si decide se usare un wildcard e quale tipo di wildcard è più appropriato. La lista seguente fornisce le linee guida da seguire:

* Una variabile "In" è definita con un upper bounded wildcard, usando la keyword `extends`
* Una variabile  "Out" è definita con un lower bounded wildcard, usando la keyword `super`
* Nel caso in cui la variabile "In" può essere acceduta usando metodi definiti nella classe `Object`, si usi un unbounded wildcard
* Nel caso in cui il codice necessiti di accedere ad una variabile e questa sia utilizzata sia per scopi "In" che "Out", allora non si deve usare un wildcard.

Queste linee guida non si applicano ai tipi di ritorno di un metodo. Usare un wildcard come tipo di ritorno di un metodo dovrebbe essere evitato in quanto costringe i programmatori ad utilizzare il codice per gestire i wildcards (type checking).


### Type Erasure

I generics sono stati introdotti nel linguaggio Java per fornire controlli di tipo più severi in fase di compilazione e per supportare la programmazione generica. Per implementare i generics, il compilatore Java applica la type erasure (cancellazione del tipo) per:

* Riampiazzare tutti i parametri di tipo con il loro bound oppure `Object` se i parametri di tipo sono unbounded. Il bytecode prodotto perciò contiene solo classi ordinarie, interfacce e metodi
* Inerire cast di tipo se necessario per preservare la sicurezza sul tipo
* Generare metodi "ponte" per preservare il polimorfismo nei tipi generici estesi.

> **Nota Bene**: La type erasure assicura che non vengano create nuove classi per tipi parametrici. Di conseguenza i generics non comportano nessun sovraccarico a runtime


### Erasure of Generics Type

Durante il processo di type erasure, il compilatore Java cancella tutti i parametri di tipo e li rimpiazza con il loro primo bound se il parametro è bounded oppure con `Object` se il parametro è unbounded.

Consideriamo il seguente codice:

```java
public class Node<T> {

    private T data;
    private Node<T> next;

    public Node(T data, Node<T> next) {
        this.data = data;
        this.next = next;
    }

    public T getData() { return data; }
    // ...
}
```

Poichè il parametro di tipo `T` è unbounded, il compilatore java lo rimpiazza con `Object`.


```java
public class Node {

    private Object data;
    private Node next;

    public Node(Object data, Node next) {
        this.data = data;
        this.next = next;
    }

    public Object getData() { return data; }
    // ...
}
```

Nell'esempio seguente la classe nodo generica usa un parametro di tipo bounded:

```java
public class Node<T extends Comparable<T>> {

    private T data;
    private Node<T> next;

    public Node(T data, Node<T> next) {
        this.data = data;
        this.next = next;
    }

    public T getData() { return data; }
    // ...
}
```

Il compilatore Java rimpiazza il parametro di tipo `T` con il primo bound associato, ossia `Comparable`:

```java
public class Node {

    private Comparable data;
    private Node next;

    public Node(Comparable data, Node next) {
        this.data = data;
        this.next = next;
    }

    public Comparable getData() { return data; }
    // ...
}
```


#### Erasure of Generic Methods

Il compilatore Java inoltre cancella i parametri di tipo negli argomenti di un metodo. si Consideri il seguente esempio:

```java
// Counts the number of occurrences of elem in anArray.
//
public static <T> int count(T[] anArray, T elem) {
    int cnt = 0;
    for (T e : anArray)
        if (e.equals(elem))
            ++cnt;
        return cnt;
}
```
Siccome `T` è unbounded, il compilatore Java replica `T` con Object:

```java
public static int count(Object[] anArray, Object elem) {
    int cnt = 0;
    for (Object e : anArray)
        if (e.equals(elem))
            ++cnt;
        return cnt;
}
```

#### Bridge Methods

Quando viene compilata una classe o un interfaccia  che estende una classe parametrizzata o implementa un'interfaccia parametrizzata, il compilatore potrebbe aver bisogno di creare un *synthetic method*, chiamato un *metodo bridge* (bridge method), come parte del processo di cancellazione. Normalmente non è necessario preoccuparsi dei metodi bridge ma potrebbe crare perplessità la presenza di uno di questi in una stack trace.

Dopo la cancellazione di tipo, le classi `Node` e `MyNode` diventano:

```java
public class Node {

    public Object data;

    public Node(Object data) { this.data = data; }

    public void setData(Object data) {
        System.out.println("Node.setData");
        this.data = data;
    }
}

public class MyNode extends Node {

    public MyNode(Integer data) { super(data); }

    public void setData(Integer data) {
        System.out.println("MyNode.setData");
        super.setData(data);
    }
}
```
Dopo la cancellazaione di tipo, la signatura del metodo `setData` non matcha. Il metodo della classe `Node` diventa `setData(Object)`, mentre il metodo della classe `MyNode` diventa `setData(Integer)`. Perciò, il metodo `setData` della classe `MyNode` non sovrascrive (override) il moetodo della classe `Node`.

Per risolvere questo problema e preservare il polimorfismo dei tipi generici dopo la cancellazione di tipo, il compilatore Java genera un metodo bridge per assicurare che il meccanismo di sottotipaggio funzioni come ci si aspetti. Per la classe `MyNode` il compilatore genera il seguente metodo bridge:

```java
class MyNode extends Node {

    // Bridge method generated by the compiler
    //
    public void setData(Object data) {
        setData((Integer) data);
    }

    public void setData(Integer data) {
        System.out.println("MyNode.setData");
        super.setData(data);
    }

    // ...
}
```
Come si può vedere, il metodo bridge che sovrascrive il metdo `setData` della classe Node, delega al metodo `setData` di MyNode.


#### Non-Reifiable Types
 Un tipo *reifiable* è un tipo le cui informazioni sul tipo sono completamente disponibili a runtime. Ciò include i primitivi, tipi non generici, raw types, e invocazioni di unbound wildcards.

I tipi *non-reifiable* sono tipi in cui le informazioni sono state cancellate a compile-time dalla cancellazione di tipo (type erasure). Ciò include invocazioni di tipi generici che non sono definti come unbounded wildcards. Un tipo non-reifiable non ha tutte le sue informazioni disponibili a runtime.


### Restriction on Generics

Per usare effetivamente i generics bisogna considerare le seguenti restrizioni:

* Non si possono istanziare tipi generici con tipi primitivi
* Non è possibile creare istanze di tipi parametrici
```java
a[i]=new T(); // error

```
* Non è possibile dichiarare campi statici i cui tipi sono parametri di tipo: il campo statico di una classe è una variabile di classe e condivisa da tutti gli oggetti (non statici) appartenenti a quella classe. Di conseguenza, i campi statici di tipo parametrico non sono consentiti.

 ```java
public class MobileDevice<T> {
    private static T os; // error
}

 ```

* Non è possibile fare cast o `istanceof` con parametri di tipo
* Non è possibile creare array di tipi parametrizzati
* Non è possibile creare, catturare o lanciare Oggetti di tipo parametrizzato
* Non è possibile overloaddare metodi che differiscono solo dal tipo generico perchè vengono prodotti metodi con la stessa signature dopo la cancellazione del tipo (type erasure):

 ```java
public class UseList<W, T> {
void processList(List<W> v) {...}
void processList(List<T> v) {...}
}

 ```
## Packages

### Creating and Using Packages

Per rendere i tipi più facili da trovare ed usare, per evitare confiltti di nome e controllare l'accesso, i programmatori
raggruppano gruppi di tipi correlati in *packages*

> **Definizione:** Un package è un raggruppamento di tipi correlati che fornisce protezione d'accesso e gestione dello spazio dei nomi.

I tipi che fanno parte della piattaforma Java sono membri di vari pacchetti che raggruppano classi per funzione.
Si dovrebbero raggruppare classi correlate in un package in quanto:

* Si capisce facilmente che i tipi sono correlati
* Si sa dove trovare le funzionalità relative alle classi del pacchetto essendo tutte raggruppate insieme
* I nomi dei tipi non entrano in confiltto con i nomi dei tipi in altri packages in quanto un package crea un nuovo namespace
* E possibile consentire ai tipi all'interno del package di avere accesso illimitato l'uno all'altro, ma limitare l'accesso per tipi esterni al package

### Creating a Package

Per creare un package, scegli un nome per il pacchetto (name conventions prossimo paragrafo) e inserisci il *package* statement con quel nome all'inizio di ogni file sorgente che contiene tipi (classi, interfacce, enumerazioni e annotazioni) che si vuole includere nel pacchetto.
Ci può essere un solo package statement per ogni file sorgente e si applica a tutti i tipi nel file.

```java
//int the Rectangle.java file
package graphics;

public class Rectangle {
    ...
}
```

> **Nota:** Se si inseriscono più tipi in un singolo file sorgente (più classi ecc.), solo uno può essere marcato pubblico e **deve** avere lo stesso nome del file sorgente. Si possono includere tipi *non-public* nello stesso file di un tipo public (è fortemente sconsigliato), ma solo il tipo pubblico sarà accessibile dall'esterno del pacchetto. Gli altri tipi non-public saranno marcati di *package private*


### Naming a Package

Il nome dei package è scritto tutto in minuscolo per evitare conflitti con nomi di classi o interfacce.
Le aziende usano il loro nome di dominio internet inverso per iniziare i nomi dei pacchetti: ad esempio `it.cashsrl.mypackage` per un pacchetto denominato *mypackage* creato da un programmatore su *cashsrl.it*.

In alcuni casi, il nome di dominio Internet potrebbe non essere un nome di pacchetto valido. Ciò può verificarsi se il nome di dominio contiene un trattino o un altro carattere speciale, se il nome del pacchetto inizia con una cifra ecc. In questo caso, la convenzione suggerita è di aggiungere un carattere di sottolineatura. Per esempio:

Domain Name|Package Name Prefix
---------------|-----------
hyphenated-name.example.org  | org.example.hyphenated_name
example.int | int_.example
123name.example.com | com.example._123name



### Using Package Members

I tipi che compongono un package sono noti come *membri del package*.
Per usare un membro pubblico del package all'esterno del package, si deve fare una delle seguenti:

* Fare riferimento al membro con il suo nome completo
* Importare il membro del package
* Importare l'intero pacchetto del membro

Ognuno è appropriato per situazioni differenti, come spiegato di seguito.

#### Referring to a Package Member by Its Qualified Name

È possibile utilizzare il nome semplice di un membro del pacchetto se il codice che si sta scrivendo si trova nello stesso pacchetto di quel membro o se quel membro è stato importato. Tuttavia, se si sta tentando di utilizzare un membro da un pacchetto diverso e tale pacchetto non è stato importato, è necessario utilizzare il nome completo del membro, che include il nome del pacchetto:

``` java
graphics.Rectangle myRect = new graphics.Rectangle(); // no package import
```

#### Importing a Package Member

Per importare uno specifico membro nel file corrente, si deve inserire un `import` statement all'inizio del file prima di qualsiasi definizione di tipo ma dopo lo statement di dichiarazione del package.


```java
import graphics.Rectangle;

Rectangle myRect = new Rectangle();
```

Questo approccio va bene se si usa giusto qualche membro del package graphics. Se invece si usano molti tipi contenuti nel package allora si dovrebbe importare l'intero package.

#### Importing an Entire Package

Per importare tutti i tipi contenuti in un package, si usa lo statement di import con l'asterisco:

```java
import graphics.*;
```

Ora ci si può riferire a qualsiasi classe del package usando il suo nome semplice.
> **Nota:** L'asterisco nell'istruzione di import può essere utilizzato solo per specificare tutte le classi all'interno di un package, come mostrato qui. Non può essere utilizzato per abbinare un sottoinsieme delle classi in un package.


#### Apparent Hierarchies of Packages

Apparentemente sembra che i packages siano gerarchici. Per esempio l'API JAva include un package `java.awt`, un package `java.awt.color`, `java.awt.font` ecc. Tuttavia tutti i packages `java.awt.xxxx` non sono inclusi nel pacchetto `java.awt`. Il prefisso `java.awt` (Java Abstract Window Toolkit) viene utilizzato per un numero di pacchetti correlati per rendere evidente la relazione, ma non per mostrare l'inclusione.

L'importazione di `java.awt.*` importa tutti i tipi del pacchetto java.awt, ma non importa `java.awt.color`, `java.awt.font` o altri pacchetti `java.awt.xxxx`. Se si prevede di utilizzare classi e altri tipi in `java.awt.color` e in `java.awt`, è necessario importare entrambi i pacchetti con tutti i relativi file:

```java
import java.awt.*;
import java.awt.color.*;

```

#### Name Ambiguities

Se un membro in un pacchetto condivide il suo nome con un membro in un altro pacchetto e entrambi i pacchetti sono importati, è necessario fare riferimento a ciascun membro tramite il suo nome qualificato.

#### The Static Import Statement

È possibile usare uno statement di import statico per importare membri statici di un package evitando di inserire come prefisso il nome della classe. Per esempio, per la classe `Math`:

```java
import static java.lang.Math.Pi; // individual static mamber

import static java.lang.Math.*; // all Maths's static members

```



## Exceptions

### What Is an Exception?

Il termine eccezione è un abbreviazione per *evento eccezionale*.

> **Definizione:** Un eccezione è un evento, che si verifica durante l'esecuzione di un programma, che interrompe il normale flusso delle istruzioni del programma. Quando si verifica un errore all'interno di un metodo, il metodo crea un oggetto e lo consegna al sistema a runtime. L'oggetto, chiamato *exception object*, contiene informazioni circa l'errore, includendo il tipo e lo stato del programma quando l'errore si è verificato. La creazione di un exception object e la sua consegna al sistema a runtime è chiamato *throwing an exception* (lancio di un'eccezione).

Dopo il lancio di un'eccezione da parte di un metodo, il sistema a runtime tenta  di trovare qualcosa per gestirlo. L'insieme delle possibile "cose" per gestire l'eccezione è l'elenco ordinato di metodi che sono stati chiamati per arrivare al metodo in cui si è verificato l'errore. L'elenco dei metodi è noto come *call stack* ()


<p align="center">
  <img src="/img/exceptions-callstack.gif" width="350"/>
</p>
</br>


Il sistema a runtime cerca nel call stack un metodo che contiene un blocco di codice in grado di gestire l'eccezione. Questo blocco di codice è chiamato *exception handler* (gestore delle eccezioni). La ricerca inizia dal metodo in cui si è verificato l'errore e prosegue attraverso il call stack nell'ordine inverso in cui sono stati chiamati i metodi. Quando viene trovato un exception handler appropriato, il sistema a runtime passa l'eccezione al gestore. Un exception handler è considerato appropriato se il tipo di un exception object generato corrisponde (matcha) al tipo che può essere gestito dal gestore dell'eccezione.

Si dice che il gestore delle eccezioni scelto catturi (catch) l'eccezione. Se il sistema a runtime ricerca esaustivamente tutti i metodi sul call stack senza trovare un gestore dell eccezione appropriato, il sistema a runtime (e di conseguenza il programma) termina.


<p align="center">
  <img src="/img/exceptions-errorOccurs.gif" width="350"/>
</p>
</br>


### The Catch or Specify Requirement

Codice Java valido deve rispettare *the Catch or Specify Requirement*. QUesto significa che il codice che potrebbe generare delle eccezioni **deve** essere racchiuso tra uno dei seguenti:

* Un `try` statement che cattura l'eccezione. Il blocco `try` deve fornire un gestore per l'eccezione.
* Un metodo  che specifica che lui può lanciare un eccezione. il metodo deve fornire una clausola `throws` che elenca le eccezioni.

Il codice che non rispetta *the Catch or Specify Requirement* non compila.

#### The Three Kinds Of Exceptions

##### Checked Exception

Il primo di tipo di eccezione è *checked exception*. Queste sono condizioni eccezionali che un applicazioni ben scritta dovrebbe prevedere e recuperare.

> **Esempio:** Supponiamo che un'applicazione richieda all'utente un nome di file di input, quindi apre il file passando il nome al costruttore per `java.io.FileReader`. Normalmente, l'utente fornisce il nome di un file leggibile esistente, quindi la costruzione dell'oggetto `FileReader` ha esito positivo e l'esecuzione dell'applicazione procede normalmente. Ma a volte l'utente fornisce il nome di un file inesistente e il costruttore lancia `java.io.FileNotFoundException`.

Un programma ben scritto inoltre dovrebbe catturare queste eccezioni e magari notificare l'utente del possibile errore. Checked exception sono soggette al *Catch or Specify Requirements*. Tutte le eccezioni sono di tipo *checked* tranne per quelle da `Error`, `RuntimeException` e tutte le loro sottoclassi.

##### Errors (unchecked exceptions)

Il secondo tipo di eccezione è *l'errore*. Ci sono condizioni eccezzionali *esterne* all'applicazione e che l'applicazione solitamente non è in grado di prevedere o ripristinare. Gli errori non sono soggetti al *Catch or Specify Requirements*.

> **Esempio**: Supponiamo che un'applicazione apra con successo un file per l'input, ma non è in grado di leggere il file a causa di un malfunzionamento dell'hardware o del sistema. La lettura non riuscita genererà `java.io.IOError`. Un'applicazione potrebbe scegliere di rilevare questa eccezione, al fine di notificare all'utente il problema, ma potrebbe anche avere senso che il programma stampi una stack trace e poi termini.

Gli errori sono quelle eccezioni indicate da `Error` e dalle sue sottoclassi.


##### Runtime Exceptions (unchecked exceptions)

Il terzo di ti eccezione è *runtime exception*. Ci sono condizioni eccezionali interne all'applicazione, e che l'applicazione solitamente non può controllare o recuperare. Questi di solito indicano bugs di programmazione, come errori logici o uso improprio di un API.

> **Esempio:** Per esempio si consideri l'applicazione descritta precedentemente che passa un nome di un file al costruttore di `FileReader`. Se un errore logico fa in modo che venga passato `null`. come parametro al costruttore, il costruttore lancera una `UnllPointerException`. L'applicazione può gestire questa eccezione, ma probabilmente ha più senso eliminare il bug che ha causato l'eccezione.

Runtime exceptions non sono soggette al *Catch or Specify Requirements*. Runtime exceptions sono quelle indicate da `RuntimeException` e dalle sue sottoclassi.

**Errors e Runtime Exceptions sono noti collettivamente come *unchecked exceptions* **.

### The `try` Block

Il primo step nel costruire un gestore di un'eccezione è di racchiudere il codice che potrebbe lanciare un eccezzione in un blocco `try`:

```java
try {
  // code
}
//catch and finally blocks...

```

Il frammento di codice `code` contiene una o più righe che potrebbero generare un'eccezione.


### The `catch` Blocks

Si associano i gestori di eccezioni ad un blocco `try` fornendo uno o più blocchi `catch` immediatamente dopo il blocco `try`. Non può essere inserito del codice tra la fine di un blocco `try` e l'inizio del primo blocco `catch`:

```java
try {

} catch (ExceptionType name) {

} catch (ExceptionType name) {

}
```
Ogni blocco `catch` è un gestore dell'eccezione che gestisce il tipo di eccezione indicata dal suo argomento. Il tipo dell' argomento, `ExceptionType`, dichiara il tipo di eccezione che il gestore può gestire e deve essere il nome di una classe che deriva dalla classe `Throwable`. Il gestore può fare riferiemento all'eccezione con `name`.

Il blocco `catch` contiene codice che viene eseguito se e quando viene invocato un gestore. Il sistema a runtime invoca il gestore dell'eccezione quando il gestore è il primo nel call stack il cui `ExceptionType` matchi il tipo dell'eccezione lanciata. Il sistema lo considera un match corretto se l'oggetto lanciato può legalmemte essere assegnato all'argomento del gestore delle eccezioni.


#### Catching More Than One Type of Exception with One Exception Handler

Da Java SE 7 e nelle versioni successive, un singolo blocco `catch` può gestire più di un tipo di eccezione. Questa funzione può ridurre la duplicazione del codice.

Nella clausola `catch`, vanno specificati i tipi di eccezioni che il blocco può gestire e separare ogni tipo di eccezione con una barra verticale (|):

```java
catch (IOException|SLQException ex) {
   logger.log(ex);
   throw.ex;
 }
```

> **Nota:** Se un blocco `catch` gestisce più di un tipo di eccezione, il parametro catch è implicitamente `final`. Nell'esempio sopra `ex` è marcato `final` e perciò non è possibile assegnare alcun valore ad esso all'interno del blocco catch.


### The `finally` Block

Un blocco `finally` viene sempre eseguito se in precedenza è presente un blocco `try`. Questo assicura che un blocco `finally` viene eseguito anche se si verifica un eccezzione inaspettata. `finally` è utile non solo per la gestione delle eccezioni, infatti consente al programmatore di ripulire il codice (clean up code) che è stato accidentalmente ignorato da un `return`, `continue` o `break`. Mettere codice in un blocco `finally` è sempre una buona pratica, anche quando non sono previste eccezioni.

> **Importante:** il blocco `finally` è uno strumento chiave per prevenire perdite di risorse. Quando si chiude un file o si ripristinano risorse in un altro modo, bisogna inserire il codice in un blocco `finally` per assicurarsi che la risorsa venga sempre ripristinata.


### The try-with-resources Statement

Lo statement *try with resources* è un `try` statement che dichiara una o più risorse. Una *risorsa* è un oggetto che deve essere chiuso dopo che il programma "ha finito di usarla". Lo statement try-with-resourcers assicura che ogni risorsa è chiusa alla fine dello statement. Qualsiasi oggetto che implementa `java.lang.AutoCloseable`, che include tutti gli oggetti che implementano `java.io.Closeable`, possono essere usati come risorsa. Il seguente esempio legge la prima riga di un file. Usa un'istnaza di `BufferedReader` per leggere dati da un file. `BufferedReader` è una risorsa che *deve* essere chiuso dopo che il programma ha finito di leggere:

```java
/*  try (
      BufferedReader br = new BufferedReader(new FileReader(path))) {
      return br.readLine();
  }
}*/
```

In questo esempio la risorsa dichiarata nello statement try-with-resources è un `BufferedReader`. La dichiarazione dello statement appare tra parentesi tonde subito dopo la keyword `try`. La classe `BufferedReader` implementa l'interfaccia `java.lang.AutoCloseable`. Siccome l'istanza di `BufferedReader` è dichiarata all'interno di un try-with-resource statement, la risorsa verrà chiusa indipendentemente dal fatto che lo statement `try` completi normalmente o all'improvviso (lancio di un'eccezione).


### Specifyng the Exceptions Thrown by a Method

Qualche volta è meglio lasciare che un metodo "più in alto" nel call stack gestisca l'eccezione piuttosto che venga gestita ill'interno del metodo in cui è stata sollevata quell'eccezione.

Per specificare che un metodo può (ri)lanciare eccezioni, si aggiunge una clausola `throws` nella dichiarazione del metodo. La clausola `throws` comprende la keyword `throws` seguita da una lista di tutte le possibili eccezione lanciate dal metodo (separate da virgola).La clausola va inserita dopo il nome del metodo e la lista degli argomenti e prima dell'apertura della parentesi graffa che definisce lo scope del metodo.


```java
public void writeList() throws IOException, IndexOutOfBoundsExceptions {
    // method body
}
```

> **Nota:** Ricordiamo che IndexOutOfBoundsExceptions è un'eccezione uncheked; includerla nella clausola throws non è obbligatorio.

### How to Throw Exceptions

Prima di catturare un'eccezione, del codice da qualche parte deve lanciarne una. Indipendentemente da cosa lancia un'eccezione, è sempre lanciata dallo statement `thrown`.
La piattaforma Java offre numerose classi di eccezioni: tutte queste classi derivano dalla classe `Throwable`, e permettono ai programmi di differenziare tra i tipi di eccezioni che possono verificarsi durante l'esecuzione di un programma. È possibile inoltre creare delle proprie classi di eccezioni per rappresentare problemi che si presentano nella classe che si sta scrivendo. Infatti, se sei uno sviluppatore di package, dovresti creare il tuo set di eccezioni per permettare agli utenti di differenziare un errore che può accadere nel tuo package da un errori che occorrono nella piattaforma Java o altrove.

#### The `throw` Statement

Tutti i metodi usano lo statement `throw` per lanciare un eccezione. Lo statement `throw` richiede un singolo argomento: un oggetto `throwable`. Gli oggetti throwable sono istanze di qualsiasi sottoclasse di Throwable.

```java
throw someThrowableObject;
```

#### Throwable Class and Its Sublcasses

Gli oggetti che ereditano dalla classe Throwable includono sia discendenti diretti (oggetti che ereditano direttamente dalla classe Throwable) che discendenti indiretti (oggetti che ereditano da figli o nipoti della classe Throwable). La figura seguente illustra la gerarchia di classi della classe Throwable e le sue sottoclassi più significative. Come si può vedere, Throwable ha due discendenti diretti: Error ed Exception.


<p align="center">
  <img src="/img/exc.gif" width="350"/>
</p>
</br>


#### Exception Classes

La maggior parte dei programmi lancia e cattura oggetti che derivano dalla classe Exception. Un'Exception indica che si è verificato un problema, ma non si tratta di problema grave di sistema. La maggior parte dei programmi scritti generano e rilevano eccezioni anziché errori.

### Creating Exceptions Classes
 Si dovrebbero scrivere le proprie classi di eccezioni se si risonde positivamente a qualsiasi delle seguenti domande:

 * Ha bisogno di un tipo di eccezione che non è rappresentato da quelli presenti nella piattaforma Java?
 * Aiuterebbe gli utenti poter differenziare le tue eccezioni da qualle generate da classi scritte da altri?
 * Se usi le eccezioni scritte da qualcun altro, gli utenti avranno accesso a tali eccezioni?


## Basic I/O

### I/O Streams

Uno I/O stream rappresenta un sorgente di input o una destinazione di output. Uno stream può rappresentare differenti tipi di sorgenti e destinazioni, inclusi file su disco, dispositivi, altri programmi ed array di memoria.
Gli stream supportano differenti tipi di dati, come semplici byte, tipi primitivi, caratteri localizzati e oggetti. Alcuni stram semplicemente trasmettono semplicemente dati. Altri manipolano e trasformano i dati in modi utili. Indipendentemente dal modo funzionamento interno, tutti gli stream lo stesso semplice modello ai programmi che li usano: uno stream è una sequenza di dati.
Un programma utilizza un input stream per leggere i dati da una sorgente, un elemento per volta.



<p align="center">
  <img src="/img/io-ins.gif" width="350"/>
</p>
</br>


Un programma usa un output stream per scrivere dati verso una destinazione, un elemento alla volta.


<p align="center">
  <img src="/img/io-outs.gif" width="350"/>
</p>
</br>



La `java.io` è divisa in due gerarchie di classi importanti a seconda del dato su cui operano: stream su byte o su carattere.


<p align="center">
  <img src="/img/javaIO.png" width="500"/>
</p>
</br>


**Data sink Streams:** funzionalità per lettura/scrittura da un supporto (es. rete, memoria, file). **Tipi**: memoria, file, pipe.
**Byte stream Input:**: `FileInputStream`, `PipedInputStream`, `ByteArrayInputStream`, `StringBufferInputStream`,
**Byte stream Output:** `FileOutpuStream`, `PipedOutputStream`, `ByteArrayOutputStream`.
**Character stream Input:**: `CharArrayReader`, `FileReader`, `PipedReader`, `StringReader`
**Character stream Output:** `CharArrayWriter`, `FileWriter`, `PipedWriter`, `StringWriter`

**Processing streams:** usati in congiunzione ai data sink streams per aggiungere ulteriori funzionalità. **Tipi**: bufferizzate, data, Object I/O.





### Byte Streams

I programmi usano byte streams per eseguire input e output di byte. Tuttel le classi byte stream discendono da `InputStream` e `OutputStream`. Ci sono molte classi di byte stream. In questo esempio ci focalizziamo su `FileInputStream` e `FileOutpuStream`.

```java
public class CopyBytes {
    public static void main(String[] args) throws IOException {

        FileInputStream in = null;
        FileOutputStream out = null;

        try {
            in = new FileInputStream("xanadu.txt");
            out = new FileOutputStream("outagain.txt");
            int c;

            while ((c = in.read()) != -1) {
                out.write(c);
            }
        } finally {
            if (in != null) {
                in.close();
            }
            if (out != null) {
                out.close();
            }
        }
    }
}
```

`CopyBytes` spende la maggior parte del tempo in un semplice ciclo che legge lo stream di input e scrive lo stream di output, un byte alla volta, come mostrato in figura:


<p align="center">
  <img src="/img/byteStream.gif" width="350"/>
</p>
</br>


La chiusura di uno stream quando non è più necessario è molto importante tanto che si usa un blocco `finally` per garantire che gli stream vengano chiusi come nell'esempio. Questa pratica aiuta ad evitare gravi perdite di risorse.

#### When Not to Use Byte Streams

Byte strams dovrebbero essere usati solamente per l'I/O più primitivo.


### Character Streams

La piattaforma Java memorizza i valori dei caratteri utlizzando le convenzioni *Unicode*. L'I/O dello stream di caratteri traduce automaticamente questo formato *in* e dal *set* di caratteri locale. Nelle versioni occidentali, il set di caratteri locali è in genere un 8-bit superset di ASCII.

Per la maggior parte delle applicazioni, l'I/O con stream di caratteri non è più complesso di quello con stream di byte. Input e output eseguiti con le classi di stream traducono automaticamente da e verso il set di caratteri locali. Se l'internazionalizzazione non è una priorità, si possono semplicemente usare le class di stream di caratteri senza porre molta attenzione ai problemi relativi ai set di caratteri. Successivamente, se l'internazionlizzazione diventa una priorità, il programma può essere adattato senza una estesa ricodifica.


#### USing Character Streams

Tutte le classi di stream di caratteri discendono da `Reader` e `Writer`. Come per gli stream di byte, ci sono classi di stream di caratteri specializzate in I/O di file: `FileReader` e `FileWriter`. L'esempio mostra l'utilizzo di queste classi:

```java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class CopyCharacters {
    public static void main(String[] args) throws IOException {

        FileReader inputStream = null;
        FileWriter outputStream = null;

        try {
            inputStream = new FileReader("xanadu.txt");
            outputStream = new FileWriter("characteroutput.txt");

            int c;
            while ((c = inputStream.read()) != -1) {
                outputStream.write(c);
            }
        } finally {
            if (inputStream != null) {
                inputStream.close();
            }
            if (outputStream != null) {
                outputStream.close();
            }
        }
    }
}
```

### Buffered Streams

Fino ad ora si è trattato di *unbuffered* I/O. Questo significa che ogni richiesta di lettura o scrittura viene gestita direttamente dal sistema operativo. Questa situazione rende un programma meno efficiente, dal momento che ciascuna di tali richieste spesso attiva l'accesso al disco, l'attività di rete o qualche altra operazione relativamente costosa.

Per ridurre questo tipo di sovraccarico, la piattafomra Java implementa i *buffered I/O streams*. I buffered input streams leggono dati da un area di memoria conosciuta come **buffer**. Un programma può convertire uno stream non bufferizzato in un buffered stream usando la pratica di wrapping già visto in precedenza, dove l'oggetto stream non bufferizzato viene passato al costruttore di una classe buffered stream:

```java
inputStream = new BuffereReader(new FileReader("file.txt"));
outputStream = new BufferedWriter(new FileWriter("out.txt"));
```

Ci sono 4 classi di streram bufferizzati usate per wrappare stream non bufferizzati:

* `BufferedInputStream` e `BufferedOutputStream` creano streams di byte bufferizzati
* `BufferedReader e BufferedWriter` creano streams buffereizzati di caratteri

#### Flushing Buffered Streams

Spesso ha senso fare in modo che tutto il contenuto del buffer vengo scritto senza aspettare che si riempia. Questo è conosciuto come *flushing the buffer*. Alcune classi di output bufferizzate supportano l'autoflush, specificato da un argomento opzionale del costruttore. Quando l'autoflush è abilitato, alcuni eventi chiave causano ol flush del buffer. Per esempio, un oggetto autoflush `PrinterWriter` flusha il buffer ad ogni invocazione di `println` o `format`.
Per flushare uno stream manualmente bisogna invocare il suo metodo `flush`. Il metodo `flush` è valido per qualsiasi stream di output, ma non ha effetto se lo stream non è bufferizzato.


### Scanning and Formatting

La programmazione I/O spesso implica la traduzione da e verso dati ben formattati con cui gli umani amano lavorare. Per assistere i programmatori relativamente a queste faccende, la piattaforma Java fornisce due API. La `scanner` API spezza l'input in **tokens** associati ai bits di dati. La `formatting` API assembla i dati in forma piacevolmente leggibile, in forma leggibile per gli "umani".

#### Scanning

Gli oggetti di tipo `Scanner` sono utili per spezzare input formattati in tokens e tradurre i singoli token in base al loro tipo di dati


> **Definizione:** I tokens sono i vari elementi di un programma Java che sono identificati dal compilatore. Un token il più piccolo elemtno di un programma significativo per il compilatore. I token supportati in Java includono keywords, variabili, costanti, caratteri speciali, operazioni ecc.


<p align="center">
  <img src="/img/token.gif" width="350"/>
</p>
</br>


##### Breaking Input into Tokens

Di default, uno scanner usa gli spazi bianchi per separare i tokens. (Un carattere bianco include blanks, tabs e terminatore di linea. Vedi `Character.isWhitespace`). Per vedere come uno scanner lavora, vediamo il seguente esempio.

```java
import java.io.*;
import java.util.Scanner;

public class ScanXan {
    public static void main(String[] args) throws IOException {

        Scanner s = null;

        try {
            s = new Scanner(new BufferedReader(new FileReader("xanadu.txt")));

            while (s.hasNext()) {
                System.out.println(s.next());
            }
        } finally {
            if (s != null) {
                s.close();
            }
        }
    }
}
```
Si noti che `ScanXan` invoca il metodo `close` quando ha finito con l'oggetto scanner. Anche se uno scanner non è uno stream, è necessario chiuderelo per indicare che si è finito di lavorare con lo stream sottostante.

L'output di `ScanXan` è il seguente:

```java
In
Xanadu
did
Kubla
Khan
A
stately
pleasure-dome
...
```

Per usare un differente separatore di tokem, si invochi `useDelimeter()`, specificando un'espressione regolare.

##### Translating INdividual Tokens

L'esmepio qui sopra tratta tutti gli input tokens come semplici stringhe di valori. Uno scanner supporta anche tokens per tutti i tipi primitivi del linguaggio Java, ade eccezione di `char`, `BigInteger e BigDecimal`


#### Formatting

Gli oggetti stream che implementato la formattazione sono istanze di `PrintWriter`, una classe di stream di caratteri, o `PrintStream`, una classe di byte stream.

> **Nota:**  Gli unici oggetti di tipo `PrintStream` di cui si ha probabilmente bisogno sono `System.out` e `System.err`. Quando si ha bisogno di creare un output stream formattato, è consigliato istanziare `PrintWriter` e non `PrintStream`.

Come per tutti gli oggetti di stream di byte o di caratteri,le istanze di `PrintWriter` e `PrintStream` implementano un set standard di metodi di scrittura per output di semplici byte o di caratteri. In più, sia `PrintWriter` che `PrintStream` implementano lo stesso insieme di metodi per convertire dati interni in output formattato. SOno disponibili due livelli di formattazione:

* `print` e `println` formattano singoli valori in modo standard
* `format` formatta quasi qualsiasi numero o valore basato su un formato stirnga, con molte opzioni per formattazioni precise.

```java
System.out.format("The square root of %d is %f.%n", i, r);
```

Tutti gli specificatori di formato iniziano con `%` e terminano con una conversione di 1 o 2 caratteri che specifica il tipo di output formattato generato. Le tre conversioni utilizzate qui sono:

* `d` formatta un valore intero come valore decimale
* `f` fomratta un valore in virgola mobile come valore decimale
* `n` stampa un terminatore di linea specifico per la piattaforma

Altre conversioni:

* `x` formatta un numero intero come un valore esadecimale
* `s` formatta qualsiasi valore come stringa


### I/O from the Command Line

Un programma viene spesso eseguito da riga di comando e interagisce con l'utente dariga di comando. La piattaforma Java supporta questo tipo di interazione in due modi: attraverso stream standard e attraverso la console.

#### Standard Streams

Gli standard stream sono una funzionalità di molti sistemi operativi. Di default, leggono l'input dalla tastiera e scrivono l'output sul display. Inoltre supportano L'I/O su file e tra programmi, ma tale funzionalità è controllata dall'interprete della riga di comando, non dal programma.


La piattaforma Java supporta tre stream standard:

* **Standard Input** accessibili tramite `System.in`
* **Standard Output** accessibile tramite `System.out`
* **Standard Error** accessibile tramite `System.err`

Questi oggetti sono definiti automaticamente e non devono essere aperti. Standard Output e Standard Error sono entrambi di output. Ci si potrebbe aspettare che gli stram standard siano stream di caratteri, ma, per ragioni storiche, sono stream di byte. `System.out` e `System.err` sono definiti come oggetti `PrintStream`. Sebbene sia tecnicamente uno stream di byte, `PrintStream` utilizza un oggetto di character stream interno per emulare molte delle caratteristiche degli stream di caratteri. Al contrario `System.in` è uno stram di byte senza funzionalità di stream di caratteri. Per utilizzare l'input standard come stream di carattere basta wrappare `System.in` in `inputStreamReader`.


### Data Streams

Data Streams supportano I/O binario di valori di tipo primitivo (`boolean`, `char`, `byte`, `short`, `int`, `long`, `float`, and `double`) come anche valori di tipo `String`. Tutti i data stream implementano l'interfaccia `DataInput` o l'interfaccia `DataOutput`.


### Objects Streams

Proprio come gli stream di dati supportano I/O di tipi di dati primitivi, gli stream di oggetti supportano I/O di oggetti. La maggior parte, ma non tutte, delle classi standard supportano la serializzazione dei loro oggetti, ossia implementano la marker interface Serializable.

Le classi di stream di oggetti sono `ObjectInputStream` e `ObjectOutputStream`. Queste classi implementano `ObjectInput` e `ObjectOutput`, che sono sottointerfacce di `DataInput` e `DataOutput`. Questo significa che tutti i metodi di I/O di dati primitivi trattati in `DataStreams` sono implementati anche negli stream di oggetti. Di conseguenza uno stream di oggetti può contenere un mix di valori primitivi e oggetti.


### File


## Concurrency

### Process and Threads

Nella programmazione concorrente ci sono due unità di base esecuzione: *processi* e *threads*. Nel linguaggio di programmazione Java, la programmazione concorrente riguarda principalmente i thread.

Un computer normalmente ha molti processi e thread attivi. Questo vale anche per sistemi con un singolo core di esecuzione e quindi hanno solo un thread che sta eseguendo in un dato momento. *Il tempo di elaborazione* per un singolo core è condiviso tra preocessi e thread attraverso una funzionalità del OS chiamata *time slicing*.

#### Processes

Un processo ha un proprio ambiente di esecuzione. In generale un processo ha un set completo e privato di risorse di base per l'esecuzione; in particolare, ogni processo ha il proprio spazio di memoria.

I processi sono spesso visti come sinonimi di programmi o applicazioni. Tuttavia, ciò che l'utente vede come singola applicazione potrebbe in effetti essere un insieme di processi cooperanti. Per facilitare la comunicazione tra i processi, la maggior parte dei sistemi operativi supporta le risorse *Inter Process Communication (IPC)*, come pipes e sockets. IPC è viene utilizzato non solo per la comunicazione tra i processi sullo stesso sistema ma anche per processi su sistemi differenti.

La maggior parte delle implementazioni della Java virtual machine viene eseguita come un singolo processo. Un'applicazione Java può creare processi aggiuntivi usando l'oggetto `ProcessBuilder`.


#### Threads

I thread sono talvolta chiamati *lightweight processes*. Sia processi che threads forniscono un ambiente di esecuzione, ma la creazione di un nuovo thread richiede meno risorse rispetto alla creazione di un nuovo processo.

I threads esistono all'interno di un processo (ogni processo ne ha almeno uno), I threads condividono le risorse del processo, inclusi memoria e file aperti. Questo rende la comunicazione efficiente, ma potenzialmente problematica.

L'esecuzione multithread è una caratteristica essenziale della piattaforma Java. Ogni applicazione ha almeno un thread (o diversi, se si contano thread di sistema che fanno cose come la gestione della memoria), il *main* thread. QUestro thread ha la capacità di creare thread aggiuntivi.

#### Thread Objects

Ogni thread è associato ad un istanza della classe `Thread`. Ci sono due strategi di base per usare oggetti di tipo `Thread` per creare un'applicazione concorrente:

* Per controllare direttamente la creazione e la gestione dei thread si istanzia semplicemente la classe `Thread` ogni qualvolta l'applicazione ha bisogno di cominciare un task asincrono.
* Per astrarre la gestione dei thread dal resto dell'applicazione, si passano i task dell'applicazioen ad  un **executor**.


#### Defining and Starting a Thread

Un'applicazione che crea un'istanza di `Thread` deve fornire il codice che verrà eseguito in tale thread. Ci sono due modi per farlo:

* Fornire un oggetto `Runnable`. L'interfaccia `Runnable` definisce un singlol metodo, `run`, pensato per contenere il codice eseguito in un thread. L'oggetto `Runnable` è passato al costruttore di `Thread`, come nell'esempio:

```java
public class HelloRunnable implements Runnable {

    public void run() {
        System.out.println("Hello from a thread!");
    }

    public static void main(String args[]) {
        (new Thread(new HelloRunnable())).start();
    }

}
```

* Estendere la classe `Thread`. La classe stessa `Thread` implementa `Runnable`, sebbene il suo metodo `run` non faccia nulla. Un'applicazione può estendere la classe `Thread`, fornendo la sua implementazione del metodo `run`, come nell'esmepio:


```java
public class HelloThread extends Thread {

    public void run() {
        System.out.println("Hello from a thread!");
    }

    public static void main(String args[]) {
        (new HelloThread()).start();
    }

}
```

**Quale modo usare?**: il primo approccio, che separa l'attività `Runnable` dall'oggetto `Thread` che esegue l'attività. Questo approccio non solo è più flessibile, ma è applicabile alle API di gestione dei thread di alto livello trattate in seguito.


#### Pausing Execution with Sleep

`Thread.sleep` fa in modo che il thread corrente sospenda l'esecuzione per un periodo specificato. QUesto è un mezzo efficiente per rendere il tempo del porcessore disponibile ad altri thread di un'applicazione o ad altre applicazioni che potrebbero essere in esecuzione in un sistema informatico. Il metodo `sleep` può essere utilizzato anche per il pacing, come nell'esempio che segue, e aspettare  un altro thread. Sono fornite due versioni di `sleep`: una specifica il tempo in millisecondi, l'altra in nanosecondi. Tuttavia, questi tempi di `sleep` non è garantito che siano precisi, in quanto sono limitati dalle strutture fornite dal sistema operativo sottostante. Inoltre il periodo di `sleep` può terminare a causa di un interrupt. In ogni caso, non è possibile assumereche l'invocazione del metodo `sleep` sospenderà il thread per il tempo specificato.


```java
public class SleepMessages {
    public static void main(String args[]) throws InterruptedException {
        String importantInfo[] = {
            "Mares eat oats",
            "Does eat oats",
            "Little lambs eat ivy",
            "A kid will eat ivy too"
        };

        for (int i = 0; i < importantInfo.length; i++) {
            //Pause for 4 seconds
            Thread.sleep(4000);
            //Print a message
            System.out.println(importantInfo[i]);
        }
    }
}
```

#### Interrupt

Un *interrupt* è un indicazione a un thread che dovrebbe interrompere ciò che sta facendo e fare qualcos'altro. Spetta al programmatore decidere esattamente come un thread debba rispondere ad un interrupt, ma è comune per un thread terminare a causa di un interrupt.

Un thread invia un interrupt invocando un `interrupt` sull'oggetto `Thread` per il thread da interrompere. Per garantire che il meccanismo di interrupt funzioni correttamentem il thread interrotto deve supportare la propria interruzione.


##### Supporting Interruption

Come un thread supporta un interruzzione? Dipende da cosa sta facendo. Se il thread sta frequentemente invocando metodi che lanciano `InterruptedException`, allora ritorna semplicemente dal metodo `run` dopo aver catturato quell'eccezione.


```java
for (int i = 0; i < importantInfo.length; i++) {
    // Pause for 4 seconds
    try {
        Thread.sleep(4000);
    } catch (InterruptedException e) {
        // We've been interrupted: no more messages.
        return;
    }
    // Print a message
    System.out.println(importantInfo[i]);
}
```

Molti metodi che lanciano `InterruptedException`, come sleep, sono progettati per annulare le operazioni correnti e ritornare immediatamente quando viene ricevuto un interrupt.

Cosa succede se un thread va avanti molto tempo senza richiamare un metodo che genera un `InterruptedException`? In questo caso deve periodicamente richiamare `Thread.interrupted`, che restituisce `true` se è stato ricevuto un interrupt.

```java
for (int i = 0; i < inputs.length; i++) {
    heavyCrunch(inputs[i]);
    if (Thread.interrupted()) {
        // We've been interrupted: no more crunching.
        return;
    }
}
```

In questo esempio, il codice verifica semplicemente l'interrupt ed esce dal thread se ne è stato ricevuto uno. Nelle applicazioni più complesse, potrebbe essere più sensato lanciare un'interrupt.

```java
if (Thread.interrupted()) {
    throw new InterruptedException();
}
```

##### The Interrupt Status Flag

Il meccanismo di interruzione è implementato utilizzando un flag interno noto come *stato dell'interrupt*. Invocando `Thread.interrupt` imposta questo flag. Quando un thread verifica la presenza di un interrupt invocando il metodo statico `Thread.interrupted`, lo stato dell'interrupt viene cancellato. Il metodo non statico `isInterrupted`, usato da un thread per interrogare lo stato di interrupt di un altro, non modifica il flag di stato dell'interrupt. Per convenzione, qualsiasi metodo che esce a causa del lancio di un `InterruptedException` cancella lo stato di interrupt quando lo fo. Tuttavia è sempre possibile che lo stato di un interrupt sia immediatamente reimpostato da un altro thread che richiama l'interrupt.



#### Joins

Il metodo `join` permette ad un thread di aspettare il completamento di un altro thread. Se `t` è un oggetto di tipo `Thread`, il cui thread è attualmente in esecuzione,

```java
t.join();
```

fa in modo che il thread corrente sospenda l'esecuzione fino a quando il thread `t` termina. Overlaods di join permettono ai programmatori di specificare un periodo di attesa. Tuttavia, come per sleep, join dipende dal OS per quanto riguard il tempo, quindi non si dovrebbe presumere che il join attenderà esattamente quanto specificato.

Come per `sleep`, `join` risponde ad un interrutp uscendo con una `InterruptedException`.



### Synchronization

I thread comunicano principalmente condividendo l'accesso ai campi e ai rifermenti agli oggetti a cui si riferiscono. Questa form adi comunicazione è estremamente efficiente, ma rende possibili due tipi di errori: *interfernza tra thread* ed *errori di consistenza della memoria*. Lo strumento necessario per prevenire questi errori è la *synchronization*.

Tuttavia, la sincronizzazione può introdurre conflitti tra thread, che si verificano quando due o piu thread tentano di accedere contemporaneamente alla stessa risorsa e fanno sì che la Java runtime esegua uno o più thread più lentamente, o addirittua sospenda la loro esecuzione. *Starvatione* e *livelock*
sono forme di contesa tra thread.

#### Thread Interference

Si con consideri una semplice classe `Counter`

```java
class Counter {
    private int c = 0;

    public void increment() {
        c++;
    }

    public void decrement() {
        c--;
    }

    public int value() {
        return c;
    }

}
```

`Counter` è progettata in modo tale che ogni invocazione di `increment` aggiunge un 1 a `c`, ed ogni invocazione di `decrement`, sottrae un 1 a `c`. Tuttavia, se un oggetto `Counter` e riferito da più threads, l'interferenza tra threads potrebbe impedire che ciò accada come previsto.

L'interferenza si verifica quando due operazioni, eseguite su threads differenti, ma che agiscono sugli stessi dati, si alternano. Ciò significa che le due operazioni consistono di molti passaggi, e le sequenze di passaggi si sovrappongono.

Potrebbe non sembrare possibile per operazioni su istanze di Counter avere delle alternanze, dal momento che entrambe le operazioni su c sono semplici singole dichiarazioni. Tuttavia, anche semplici statements posso tradursi in più operazioni svolte dalla virtual machine. Infatti, la singola espressione `c++` può essere scomposta in tre passaggi:

* Recupera il valore corrente di c
* Incrementa il valore recuperato di 1
* Memorizza il valore incrementato

Supponiamo che il thread A invochi l'incremento all'incirca nello stesso momento in cui il thread B richiama il decremento. Se il valore iniziale di c è 0, le loro azioni potrebbero alternarsi nel seguente modo:

* **Thread A**: recupera c
* **Thread B**: recupera c
* **Thread A**: incrementa il valore recuperato, il risultato è 1
* **Thread B**: decrementa il valore recuperato, il risultato è -1
* **Thread A**: salva il risultato in c, ed ora c = 1
* **Thread B**: salva il risultato in c, ed ora c = -1

Il risultato del thread A è perso, sovrascritto dal thread B. Questa particolare alternanza è solo una delle possibilità. In circostanze diverse potrebbe essere il risultato del thread B che si perde, o non ci può essere alcun errore. Poiché sono imprevedibili, i bug di interferenza dei thread possono essere difficili da rilevare e risolvere.


#### Memory Consistency Errors
Errori di inconsistenza della memoria accadono quando thread distinti hanno viste differenti di quelli che dovrebbero essere gli stessi dati. Le cause di questi errori sono complesse. La chiave per evitare errori di coerenza di memoria è capire la relazione *happens-before*.
Questa relazione è semplicemente una garanzia che la memoria scritta da uno specifico statement è visibile da un altro specifico statement. Esempio:

```java
int counter = 0;
```

Il campo counter è condiviso tra due threads, A e B. Suppoiniamo di incrementare A:

```java
counter++;
```

Poi, subito dopo, il thread B stampa `counter`:

```java
System.put.println(counter);
```

Se i due statements sono eseguiti nello stesso thread, è corretto pensare che il valore stampato sia 1. Ma se i due statements sono eseguiti su due thread differenti, il valore stampato potrebbe non essere `0`, in quanto non c'alcuna garanzia che il cambiamento provocato dal thread A sia visibile al thread B, a meno che il porgrammatore abbia stabilito una relazione *happens-before* tra questi due statements.

Ci sono molti modi per creare relazioni happens-before. Uno di questi è la sincronizzazione.


#### Synchronized Methods

Java fornisce due modi base di sincronizzazione: i metodi sincronizzati e gli statements sincronizzati.

Per rendere un metodo sincronizzato, semplicemente si aggiunge la keyword `synchronized` alla sua dichiarazione, prima del tipo di ritorno:

```java
public class SynchronizedCounter {
    private int c = 0;

    public synchronized void increment() {
        c++;
    }

    public synchronized void decrement() {
        c--;
    }

    public synchronized int value() {
        return c;
    }
}
```
Se count è un istanza di `SynchronizedCounter`, allora rendendere questi metodi sincronizzati provaca 2 cose:

* La prima, non sono possibile scambi per due invocazioni di metodi sincronizzati sullo stesso oggetto. Quando un thrad sta eseguendo un metodo sincronizzato per un oggetto, tutti gli altri thread che invocano metodi sincronizzati sullo stesso oggetto sospendono la loro esecuzione fino a quando il primo thread non ha finito con l'oggetto.
* Secondo, quando esiste un metodo sincronizzato, automaticamente stabilisce una relazione happens-before con qualsiasi successiva invocazione di un metodo sincronizzato sullo stesso oggetto. QUesto garantisce che i cambiamenti sullo stato di un oggetto siano visibili a tutti i threads.

Si noti che i costruttori non possono essere sincronizzati. Sincronizzare i costruttori non ha senso in quanto solo il thread che crea un oggetto dovrebbe avere accesso al costruttore mentre viene costruito.

I metodi sincronizzati abilitano una strategia semplice per prevenire l'interferenza dei thread e gli errori di coerenza della memoria: se un oggetto è visibile a più thread, tutte le letture o le scritture sulle variabili di quell'oggetto vengono eseguite tramite metodi sincronizzati. (Un'eccezione importante: i campi `final`, che non possono essere modificati dopo che l'oggetto è stato costruito, possono essere tranquillamente letti attraverso metodi non sincronizzati, una volta costruito l'oggetto) Questa strategia è efficace, ma può presentare problemi di liveness.


#### Intrinsic Lock and Synchronization

La sincronizzazione è costruita attorno ad un'entità interna nota come `intrinsic lock` o `monitor lock`. (Le API si riferiscono a questa entità come "monitor"). Gli Intrinsic lock giocano un ruolo in entrambi gli aspetti della sincronizzazione: rafforzano l'accesso esclusivo allo stato di un oggetto e stabiliscono relazioni happens-before che sono essenziali per la visibilità.

Ogni oggetto ha un intrinsick lock associato ad esso. Per convenzione, un thread che necessita di un accesso esclusivo e consistente ad un campo di un oggetto deve acquisire l'intrinsic lock dell'oggetto prima di potervi accedere, e poi rilasciare il lock quando ha finito. Si dice che un thread possiede il lock dal momento in cui ha acquisito il lock fino a quando lo ha rilasciato. Finchè un thread possiede il lock, nessun altro thread può acqusire lo stesso lock. L'altro thread verrà bloccato se dovesse tentare di acquisire il lock.

Quando un thread rilascia un lock, viene stabilita una relazione happens-before tra quell'azione e ogni successiva acquisizione dello stesso lock.


#### Locks In Sinchronized Methods

Qaundo un thread invoca un metodo sincronizzato, automaticamente acquisisce il lock per l'oggetto del metodo e lo rilascia quando il metodo ritorna. Il lock viene rilasciato anche se il return è causato da un'eccezione non rilevata.

Ci si potrebbe chiedere cosa succede quando viene invocato un metodo sincronizzato statico, poiché un metodo statico è associato a una classe e non ad un oggetto. In questo caso, il thread acquisisce il lock per l'oggetto `Class` associato alla classe. Pertanto l'accesso ai campi statici della classe è controllato da un lock che è diverso dal lock per qualsiasi istanza della classe.


#### Sinchronized Statements

Un altro modo per creare codice sincronizzato è attraverso *synchronized statements*. Diversamente dai metodi sincronizzati, gli statements sincronizzarti devono specificare l'oggetto di cui si vuole acquisire il lock.



#### Atomic Access

Nella programmazione, un'azione atomica è quella che effettivamente accade tutto in una volta. Un'azione atomica non può fermarsi nel mezzo: o accade completamente, o non accade affatto. Non sono visibili effetti collaterali di un'azione atomica finché l'azione non è completa.

Abbiamo già visto che un'espressione di incremento, come `c++`, non descrive un'azione atomica. Anche espressioni molto semplici possono definire azioni complesse che possono decomporsi in altre azioni. Tuttavia, ci sono azioni che si possono definire come atomiche:

* Lettura e scrittura sono operazioni atomiche per variabili riferimento e per la maggior parte delle variabili primitive (tutti i tipi tranne per long e double).
* Lettura e scrittura sono operazioni atomiche per tutte le variabili dichiarate `volatile` (comprese le variabili long e double).

Le azioni atomiche non possono essere intervallate, quindi possono essere utilizzate senza paura di interferenza fra thread. Tuttavia, ciò non elimina la necessità di sincronizzare le azioni atomiche, poiché errori di coerenza della memoria sono ancora possibili. L'uso di variabili volatili riduce il rischio di errori di coerenza della memoria, poiché ogni scrittura su una variabile volatile stabilisce una relazione happens-before con letture successive della stessa variabile. Ciò significa che le modifiche a una variabile volatile sono sempre visibili ad altri thread. Inoltre, significa anche che quando un thread legge una variabile volatile, non vede solo l'ultima modifica, ma anche gli effetti collaterali del codice che hanno portato alla modifica.

Accedere usando una semplice variabile atomica è più efficiente che accedere a queste variabili tramite codice sincronizzato, ma richiede una maggiore attenzione da parte del programmatore per evitare errori di coerenza della memoria. Se lo sforzo extra è utile dipende dalle dimensioni e dalla complessità dell'applicazione.

Alcune delle classi nel pacchetto java.util.concurrent forniscono metodi atomici che non si basano sulla sincronizzazione.

### Liveness

La capacità di un'applicazione concorrente di eseguire in modo tempestivo è nota come liveness. Questa sezione descrive i problemi più comuni di *liveness*, *deadlock*, e prosegue descrivendo brevemente altri due problemi di liveness, *starvation* e *livelock*.


#### DeadLock

Un Deadlock descrive una situazione in cui due o più thread sono bloccati per sempre, in attesa l'uno dell'altro. Ecco un esempio.

Alphonse e Gaston sono amici e grandi credenti nella cortesia. Una rigida regola di cortesia è che quando ti inchini ad un amico, devi rimanere inchinato finché il tuo amico non ha la possibilità di restituire l'inchino. Sfortunatamente, questa regola non tiene conto della possibilità che due amici si pieghino l'un l'altro allo stesso tempo. Questa applicazione di esempio, Deadlock, modella questa possibilità:


```java
public class Deadlock {
    static class Friend {
        private final String name;
        public Friend(String name) {
            this.name = name;
        }
        public String getName() {
            return this.name;
        }
        public synchronized void bow(Friend bower) {
            System.out.format("%s: %s"
                + "  has bowed to me!%n",
                this.name, bower.getName());
            bower.bowBack(this);
        }
        public synchronized void bowBack(Friend bower) {
            System.out.format("%s: %s"
                + " has bowed back to me!%n",
                this.name, bower.getName());
        }
    }

    public static void main(String[] args) {
        final Friend alphonse =
            new Friend("Alphonse");
        final Friend gaston =
            new Friend("Gaston");
        new Thread(new Runnable() {
            public void run() { alphonse.bow(gaston); }
        }).start();
        new Thread(new Runnable() {
            public void run() { gaston.bow(alphonse); }
        }).start();
    }
}
```

Quando viene eseguito` Deadlock`, è estremamente probabile che entrambi i thread si blocchino quando tentano di richiamare `bowBack`. Nessun blocco finirà mai, perché ogni thread sta aspettando che l'altro esca da `bow`.

#### Starvation e LiveLock

Starvation e livelock sono problemi molto meno comuni di un deadlock, ma sono comunque problemi che ogni progettista di software concorrente può incontrare.

##### Starvation

Starvation descrive una situazione in cui un thread non è in grado di ottenere un accesso regolare alle risorse condivise e non è in grado di fare progressi. Questo accade quando le risorse condivise sono rese non disponibili per lunghi periodi da thread "greedy"(avidi). Ad esempio, supponiamo che un oggetto fornisca un metodo sincronizzato che spesso richiede molto tempo per essere restituito. Se un thread richiama frequentemente questo metodo, spesso vengono bloccati anche altri thread che richiedono un accesso sincronizzato frequente allo stesso oggetto.

##### LiveLock

Un thread spesso agisce in risposta all'azione di un altro thread. Se l'azione del thread secondario è anche una risposta all'azione di un altro thread, potrebbe verificarsi un livelock. Come per la situazione di deadlock, i thread in fase di livelock non sono in grado di fare ulteriori progressi. Tuttavia, i thread non sono bloccati - sono semplicemente troppo occupati a rispondere l'un l'altro per riprendere il lavoro. Questo è paragonabile a due persone che tentano di passarsi l'un l'altro in un corridoio: Alphonse si sposta alla sua sinistra per lasciar passare Gaston, mentre Gaston si sposta alla sua destra per lasciare passare Alphonse. Vedendo che si stanno ancora bloccando a vicenda, Alphone si sposta alla sua destra, mentre Gaston si sposta alla sua sinistra. Stanno ancora bloccandosi a vicenda, quindi ...

### Guarded Blocks

I thread spesso devono coordinare le loro azioni. La pratica di coordinamento più comune è il guarded block. Tale blocco inizia verificando una condizione che deve essere vera prima che il blocco possa procedere. Ci sono una serie di passaggi da seguire per farlo correttamente.

Supponiamo, ad esempio, che `guardedJoy` sia un metodo che non deve procedere finché una vairabile `joy` condivisa non è stata settata da un altro thread. Un tale metodo potrebbe, in teoria, semplicemente eseguire il ciclo fino a quando la condizione non è soddisfatta, ma tale ciclo è dispendioso, poiché viene eseguito continuamente durante l'attesa.

```java
public void guardedJoy() {
    // Simple loop guard. Wastes
    // processor time. Don't do this!
    while(!joy) {}
    System.out.println("Joy has been achieved!");
}
```

Una guard più efficiente invoca `Object.wait` per sospendere il thread corrente. L'invocazione di `wait` non ritorna fino a quando un'altro thread ha emesso una notifica che indica che potrebbe essersi verificato qualche evento speciale, sebbene non necessariamente l'evento che questo thread sta aspettando:


```java
public synchronized void guardedJoy() {
    // This guard only loops once for each special event, which may not
    // be the event we're waiting for.
    while(!joy) {
        try {
            wait();
        } catch (InterruptedException e) {}
    }
    System.out.println("Joy and efficiency have been achieved!");
}
```

> **Nota:** invoca sempre `wait` all'interno di un ciclo che verifica la condizione in attesa.

Come molti metodi che sospendono l'esecuzione, `wait` può generare `InterruptedException`. In questo esempio, possiamo semplicemente ignorare questa eccezione: ci interessa solo il valore di `joy`.

Perché questa versione di `guardedJoy` è sincronizzata? Supponiamo che `d` sia l'oggetto che stiamo usando per invocare `wait`. Quando un thread invoca `d.wait`, deve possedere il lock per `d`, altrimenti viene generato un errore. Invocare `wait` all'interno di un metodo sincronizzato è un modo semplice per acquisirne il lock.

Quando viene richiamato `wait`, il thread rilascia il lock e sospende l'esecuzione. In futuro, un altro thread acquisirà lo stesso blocco e invocherà `Object.notifyAll`, informando tutti i thread in attesa su quel blocco che è successo qualcosa di importante:


```java
public synchronized notifyJoy() {
    joy = true;
    notifyAll();
}
```

Qualche istante dopo che il secondo thread ha rilasciato il lock, il primo thread riacquisisce il lock e riprende ritornando all'invocazione di `wait`.

> **Nota:** esiste un secondo metodo di notifica, `notify`, che risveglia un singolo thread.


Utilizziamo dei guard block per creare un'applicazione `Producer-Consumer`. Questo tipo di applicazione condivide i dati tra due thread: il produttore, che crea i dati, e il consumatore, che li consuma. I due thread comunicano usando un oggetto condiviso. Il coordinamento è essenziale: il thread del consumatore non deve tentare di recuperare i dati prima che il thread del produttore li abbia consegnati e il thread del produttore non deve tentare di fornire nuovi dati se il consumatore non ha recuperato i vecchi dati.


In questo esempio, i dati sono una serie di messaggi di testo, che sono condivisi attraverso un oggetto di tipo Drop:

```java
public class Drop {
    // Message sent from producer
    // to consumer.
    private String message;
    // True if consumer should wait
    // for producer to send message,
    // false if producer should wait for
    // consumer to retrieve message.
    private boolean empty = true;

    public synchronized String take() {
        // Wait until message is
        // available.
        while (empty) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        // Toggle status.
        empty = true;
        // Notify producer that
        // status has changed.
        notifyAll();
        return message;
    }

    public synchronized void put(String message) {
        // Wait until message has
        // been retrieved.
        while (!empty) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        // Toggle status.
        empty = false;
        // Store message.
        this.message = message;
        // Notify consumer that status
        // has changed.
        notifyAll();
    }
}
```

Il thread del produttore, definito in `Producer`, invia una serie di messaggi. La stringa `"DONE"` indica che tutti i messaggi sono stati inviati. Per simulare la natura imprevedibile delle applicazioni del mondo reale, il thread del produttore fa una pausa ad intervalli casuali tra i messaggi.

```java
import java.util.Random;

public class Producer implements Runnable {
    private Drop drop;

    public Producer(Drop drop) {
        this.drop = drop;
    }

    public void run() {
        String importantInfo[] = {
            "Mares eat oats",
            "Does eat oats",
            "Little lambs eat ivy",
            "A kid will eat ivy too"
        };
        Random random = new Random();

        for (int i = 0;
             i < importantInfo.length;
             i++) {
            drop.put(importantInfo[i]);
            try {
                Thread.sleep(random.nextInt(5000));
            } catch (InterruptedException e) {}
        }
        drop.put("DONE");
    }
}
```

Il thread del consumatore, definito in `Consumer`, recupera semplicemente i messaggi e li stampa, finché non recupera la stringa `"DONE"`. Inoltre questo thread va in pausa ad intervalli casuali.


```java
import java.util.Random;

public class Consumer implements Runnable {
    private Drop drop;

    public Consumer(Drop drop) {
        this.drop = drop;
    }

    public void run() {
        Random random = new Random();
        for (String message = drop.take();
             ! message.equals("DONE");
             message = drop.take()) {
            System.out.format("MESSAGE RECEIVED: %s%n", message);
            try {
                Thread.sleep(random.nextInt(5000));
            } catch (InterruptedException e) {}
        }
    }
}
```

Alla fine, il main thread, definito in `ProducerConsumerExample`, che lancia i thread `Producer` e `Csonsumer`.

```java
public class ProducerConsumerExample {
    public static void main(String[] args) {
        Drop drop = new Drop();
        (new Thread(new Producer(drop))).start();
        (new Thread(new Consumer(drop))).start();
    }
}
```

### Immutable Objects

Un oggetto è considerato immutabile se il suo stato non può cambiare dopo che è stato costruito. La massima dipendenza da oggetti immutabili è ampiamente accettata come una solida strategia per la creazione di codice semplice e affidabile.

Gli oggetti immutabili sono particolarmente utili in applicazioni concorrenti. Dal momento che non possono cambiare lo stato, non possono essere corrotti dall'interferenza di thread o trovarsi in uno stato incoerente.

I programmatori sono spesso riluttanti ad impiegare oggetti immutabili, perché si preoccupano del costo di creare un nuovo oggetto piuttosto di aggiornare un oggetto sul posto. L'impatto della creazione di oggetti è spesso sovrastimato e può essere compensato da alcune caratteristiche efficienti associate agli oggetti immutabili. Questi includono un ridotto overhead dovuto al garbage collection e l'eliminazione del codice necessario per proteggere gli oggetti mutabili dalla corruzione.

Le seguenti sottosezioni prendono una classe le cui istanze sono mutabili e derivano da una classe con istanze immutabili. Così facendo, forniscono regole generali per questo tipo di conversione e dimostrano alcuni dei vantaggi degli oggetti immutabili.

#### A Synchronized Class Example

La classe SynchronizedRGB, definisce oggetti che rappresentano colori. Ogni oggetto rappresenta il colore attraverso tre interi corrispondenti ai colori primari e una stringa che identifica il nome del colore.

```java
public class SynchronizedRGB {

    // Values must be between 0 and 255.
    private int red;
    private int green;
    private int blue;
    private String name;

    private void check(int red,
                       int green,
                       int blue) {
        if (red < 0 || red > 255
            || green < 0 || green > 255
            || blue < 0 || blue > 255) {
            throw new IllegalArgumentException();
        }
    }

    public SynchronizedRGB(int red,
                           int green,
                           int blue,
                           String name) {
        check(red, green, blue);
        this.red = red;
        this.green = green;
        this.blue = blue;
        this.name = name;
    }

    public void set(int red,
                    int green,
                    int blue,
                    String name) {
        check(red, green, blue);
        synchronized (this) {
            this.red = red;
            this.green = green;
            this.blue = blue;
            this.name = name;
        }
    }

    public synchronized int getRGB() {
        return ((red << 16) | (green << 8) | blue);
    }

    public synchronized String getName() {
        return name;
    }

    public synchronized void invert() {
        red = 255 - red;
        green = 255 - green;
        blue = 255 - blue;
        name = "Inverse of " + name;
    }
}

```

SynchronizedRGB deve essere usata con attenzione per evitare di entrare in uno stato di inconsistenza. Supponiamo, ad esempio, che un thread esegua il seguente codice:


```java
SynchronizedRGB color =
    new SynchronizedRGB(0, 0, 0, "Pitch Black");
...
int myColorInt = color.getRGB();      //Statement 1
String myColorName = color.getName(); //Statement 2
```

Se un altro thread richiama color.set dopo l'istruzione 1 ma prima dell'istruzione 2, il valore di myColorInt non corrisponde al valore di myColorName. Per evitare questo risultato, le due istruzioni devono essere collegate tra loro:


```java
synchronized (color) {
    int myColorInt = color.getRGB();
    String myColorName = color.getName();
}
```


Questo tipo di inconsistenza è possibile solo per oggetti mutabili: non sarà un problema per la versione immutabile di SynchronizedRGB.


#### A Strategy for Definig Immutable Objects

Le seguenti regole definiscono una strategia semplice per la creazione di oggetti immutabili. Non tutte le classi documentate come "immutabili" seguono queste regole.

* Non fornire metodi `setter` - metodi che modificano campi o oggetti cui fanno riferimento i campi.
* Rendi tutti i campi `final` e `private`
* Non consentire alle sottoclassi di sovrascrivere i metodi. Il modo più semplice per farlo è dichiarare la classe come `final`. Un approccio più sofisticato è rendere privato il costruttore e costruire istanze in factory method.
* Se i campi dell'istanza includono riferimenti a oggetti mutabili, non consentire la modifica di tali oggetti:
* * Non fornire metodi che modificano gli oggetti mutabili.
* * Non condividere riferimenti ad oggetti mutabili. Non memorizzare mai riferimenti ad oggetti esterni mutabili passati al costruttore; se necessario, creare copie e memorizzare i riferimenti alle copie. Allo stesso modo, crea copie dei tuoi oggetti interni mutabili quando necessario per evitare di restituire gli originali nei tuoi metodi.

L'applicazione di questa strategia a `SynchronizedRGB provoca` i seguenti passaggi:

* Ci sono due metodi `setter` in questa classe. Il primo, `set`, trasforma arbitrariamente l'oggetto. Il secondo, `invert`, può essere adattato facendo in modo che crei un nuovo oggetto invece di modificare quello esistente.
* Tutti i campi sono già privati e sono ulteriormente qualificati come `final`.
La classe stessa è dichiarata `final`.
* Solo un campo si riferisce ad un oggetto e quell'oggetto è esso stesso immutabile. Pertanto, non è necessaria alcuna protezione contro la modifica dello stato degli oggetti mutabili "contenuti". (non ce ne sono)

Dopo queste modifiche, abbiamo `ImmutableRGB`:

```java

final public class ImmutableRGB {

    // Values must be between 0 and 255.
    final private int red;
    final private int green;
    final private int blue;
    final private String name;

    private void check(int red,
                       int green,
                       int blue) {
        if (red < 0 || red > 255
            || green < 0 || green > 255
            || blue < 0 || blue > 255) {
            throw new IllegalArgumentException();
        }
    }

    public ImmutableRGB(int red,
                        int green,
                        int blue,
                        String name) {
        check(red, green, blue);
        this.red = red;
        this.green = green;
        this.blue = blue;
        this.name = name;
    }


    public int getRGB() {
        return ((red << 16) | (green << 8) | blue);
    }

    public String getName() {
        return name;
    }

    public ImmutableRGB invert() {
        return new ImmutableRGB(255 - red,
                       255 - green,
                       255 - blue,
                       "Inverse of " + name);
    }
}
```
### High Level Concurrency Objects

#### Lock Objects

Il codice sincronizzato si basa su un tipo semplice di *reentrant lock*. Questo tipo di lock è facile da usare, ma presenta molte limitazioni. Le pratiche di lock più sofisticate sono supportate dal pacchetto `java.util.concurrent.locks`.

Gli oggetti lock funzionano in modo molto simile ai lock impliciti utilizzati dal codice sincronizzato. Come per i lock impliciti, solo un thread può possedere un oggetto Lock alla volta. Gli oggetti Lock supportano anche un meccanismo di *wait/notify*, tramite gli oggetti `Conditions` a loro associati.

Il più grande vantaggio degli oggetti Lock a differenza degli implicits lock è la loro capacità di tornare indietro da un tentativo di acquisizione di un lock. Il metodo `tryLock` torna indietro se il blocco non è disponibile immediatamente o prima della scadenza di un timeout (se specificato). Il metodo `lockInterruptibly` torna indietro se un altro thread invia un interrupt prima che il blocco venga acquisito.

Usiamo gli oggetti Lock per risolvere il problema del deadlock che abbiamo visto in `Liveness`. Alphonse e Gaston si sono allenati per notare quando un amico sta per inchinarsi. Modelliamo questo miglioramento richiedendo che i nostri oggetti `Friend` debbano acquisire locks per entrambi i partecipanti prima di procedere con l'inchino. Ecco il codice sorgente per il modello migliorato, `Safelock`. Per dimostrare la versatilità di questo approccio, supponiamo che Alphonse e Gaston siano così infatuati della loro nuova capacità di piegarsi in modo sicuro che non possono smettere di inchinarsi l'un l'altro


```java
public class Safelock {
    static class Friend {
        private final String name;
        private final Lock lock = new ReentrantLock();

        public Friend(String name) {
            this.name = name;
        }

        public String getName() {
            return this.name;
        }

        public boolean impendingBow(Friend bower) {
            Boolean myLock = false;
            Boolean yourLock = false;
            try {
                myLock = lock.tryLock();
                yourLock = bower.lock.tryLock();
            } finally {
                if (! (myLock && yourLock)) {
                    if (myLock) {
                        lock.unlock();
                    }
                    if (yourLock) {
                        bower.lock.unlock();
                    }
                }
            }
            return myLock && yourLock;
        }

        public void bow(Friend bower) {
            if (impendingBow(bower)) {
                try {
                    System.out.format("%s: %s has"
                        + " bowed to me!%n",
                        this.name, bower.getName());
                    bower.bowBack(this);
                } finally {
                    lock.unlock();
                    bower.lock.unlock();
                }
            } else {
                System.out.format("%s: %s started"
                    + " to bow to me, but saw that"
                    + " I was already bowing to"
                    + " him.%n",
                    this.name, bower.getName());
            }
        }

        public void bowBack(Friend bower) {
            System.out.format("%s: %s has" +
                " bowed back to me!%n",
                this.name, bower.getName());
        }
    }

    static class BowLoop implements Runnable {
        private Friend bower;
        private Friend bowee;

        public BowLoop(Friend bower, Friend bowee) {
            this.bower = bower;
            this.bowee = bowee;
        }

        public void run() {
            Random random = new Random();
            for (;;) {
                try {
                    Thread.sleep(random.nextInt(10));
                } catch (InterruptedException e) {}
                bowee.bow(bower);
            }
        }
    }


    public static void main(String[] args) {
        final Friend alphonse =
            new Friend("Alphonse");
        final Friend gaston =
            new Friend("Gaston");
        new Thread(new BowLoop(alphonse, gaston)).start();
        new Thread(new BowLoop(gaston, alphonse)).start();
    }
}
```


### Executors

#### Executors Interface

Il pacchetto `java.util.concurrent` definisce tre interfacce executor:

* `Executor`, un'interfaccia semplice che supporta l'avvio di nuovi tasks
* `ExecutorService`, una subinterfaccia di Executor, che aggiunge funzionalità che aiutano a gestire il ciclo di vita, sia dei singoli task che dell'executor stesso.
* `ScheduledExecutorService`, una sottointerfaccia di ExecutorService, supporta l'esecuzione futura e / o periodica dei tasks

In genere, le variabili che fanno riferimento a oggetti executor vengono dichiarate come uno di questi tre tipi di interfaccia, non con un tipo di classe executor.

##### The `Executor` Interface

L'interfaccia di `Executor` fornisce un unico metodo, `execute`, progettato per essere un alternativa alla comune pratica di creazione di un thread. Se `r` è un oggetto Runnable ed `e` è un oggetto `Executor`, si può sostituire:

```java
(new Thread(r)).start();
```

con

```java
e.execute(r);
```

Tuttavia, la definizione di `execute` è meno specifica. In pratica crea un nuovo thread e lo avvia immediatamente. A seconda dell'implementazione di `Executor`, `execute` può fare la stessa cosa, ma è più probabile che utilizzi un worker thread esistente per eseguire `r`, o per posizionare `r` in una coda in attesa che un worker thread diventi disponibile.

Le implementazioni di `executor` in java.util.concurrent sono progettate per sfruttare appieno le interfacce `ExecutorService` e `ScheduledExecutorService` più avanzate, sebbene funzionino anche con l'interfaccia di base di `Executor`.


##### The `ExecutorService` Interface

L'interfaccia `ExecutorService` rimpiazza `execute` con un metodo `submit` simile ma più versatile.
Come `execute`, `submit` accetta oggetti `Runnable`, ma accetta anche gli oggetti `Callable`, che consentono ai task di restituire un valore. Il metodo `submit` restituisce un oggetto `Future`, che viene utilizzato per recuperare il valore restituito da `Callable` e per gestire lo stato di entrambi i task di `Callable` e `Runnable`.

`ExecutorService` fornisce anche metodi per inviare grandi raccolte di oggetti `Callable`. Infine, `ExecutorService` fornisce una serie di metodi per la gestione dell'arresto(shutdown) dell'`executor`. Per supportare l'arresto immediato, i task devono gestire correttamente gli interrupt.


#### Thread Pools

La maggior parte delle implementazioni di `executor` in `java.util.concurrent` utilizzano i `thread pool`, costituiti da thread worker thread. Questo tipo di thread esiste separatamente dai task Runnable e Callable eseguiti ed è spesso utilizzato per eseguire più task.

L'utilizzo dei worker thread riduce al minimo l'overhead dovuto alla creazione dei thread. Gli oggetti thread utilizzano una quantità significativa di memoria e, in un'applicazione su larga scala, l'allocazione e la deallocazione di molti oggetti thread crea un significativo overhead di gestione della memoria.

Un tipo comune di pool di thread pool sono i `fixed thread pool`. Questo tipo di thread ha sempre un numero specificato di thread in esecuzione; se un thread è in qualche modo terminato mentre è ancora in uso, viene automaticamente sostituito con un nuovo thread. Le attività vengono inviate al pool di thread tramite una coda interna, che contiene task extra ogni volta che ci sono più task attivi dei thread.

Un importante vantaggio del `fixed thread pool` è che le applicazioni che lo utilizzano *degradano con garbo*. Per capire questo, si consideri un'applicazione server Web in cui ogni richiesta HTTP è gestita da un thread separato. Se l'applicazione crea semplicemente un nuovo thread per ogni nuova richiesta HTTP e il sistema riceve più richieste di quelle che può gestire immediatamente, l'applicazione smetterà improvvisamente di rispondere a tutte le richieste quando il sovraccarico di tutti questi thread supera la capacità del sistema. Con un limite al numero di thread che possono essere creati, l'applicazione non servirà le richieste HTTP con la stessa rapidità con cui entrano, ma saranno servite alla stessa velocità del sistema.

Un modo semplice per creare un `executor` che utilizza un `fixed thread pool` consiste nel richiamare il costruttore tramite `new factoryFixedThreadPool` in `java.util.concurrent.Executors`. Questa classe fornisce inoltre i seguenti metodi:

* Il metodo `newCachedThreadPool` crea un executor con un pool di thread espandibile. Questo executor è adatto per applicazioni che lanciano molte attività di breve durata.
* Il metodo `newSingleThreadExecutor` crea un executor che esegue una singola attività alla volta.

Se nessuno degli executors forniti dai metodi precedenti soddisfa le proprie esigenze, la costruzione di istanze di `java.util.concurrent.ThreadPoolExecutor` o `java.util.concurrent.ScheduledThreadPoolExecutor` offre opzioni aggiuntive.


### Concurrent Collections


Il package `java.util.concurrent` include numerose aggiunte al Framework Java Collections:

* `BlockingQueue` definisce una struttura dati first-in-first-out che blocca o scade quando si tenta di aggiungere a una coda completa o di recuperare da una coda vuota.
* `ConcurrentMap` è una sottointerfaccia di `java.util.Map` che definisce utili operazioni atomiche. Queste operazioni rimuovono o sostituiscono una coppia chiave-valore solo se la chiave è presente, o aggiungono una coppia chiave-valore solo se la chiave è assente. Rendere atomiche queste operazioni aiuta a evitare la sincronizzazione. L'implementazione standard generale di `ConcurrentMap` è `ConcurrentHashMap`, che è l'analogo concorrente di HashMap.
* `ConcurrentNavigableMap` è una sottointerfaccia di `ConcurrentMap` che supporta matches approssimativi. L'implementazione standard generale di `ConcurrentNavigableMap` è `ConcurrentSkipListMap`, che è un analogo concorrente di `TreeMap`.


Tutte queste collections consentono di evitare errori di coerenza della memoria definendo una relazione happens-before tra un'operazione che aggiunge un oggetto alla collection con operazioni successive che accedono o rimuovono quell'oggetto.


### Atomic Variables

Il package `java.util.concurrent.atomic` definisce classi che supportano operazioni atomiche su singole variabili. Tutte le classi hanno metodi get e set che funzionano come letture e scritture su variabili volatili. Cioè, un `setter` ha una relazione happens-before con qualsiasi succesivo `getter` sulla stessa variabile. Anche il metodo `compareAndSet` ha queste caratteristiche di memory Consistency, così come i metodi aritmetici atomici che si applicano alle variabili atomiche intere.
