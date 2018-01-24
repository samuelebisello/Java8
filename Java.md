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

Il terzo di ti eccezione è *runtime exception*. Ci sono condizioni eccezionali intenre all'applicazione, e che l'applicazione solitamente non può controllare o recuperare. Questi di solito indicano bugs di programmazione, come errori logici o uso improprio di un API. 

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
```

> **Nota:** Se un blocco `catch` gestisce più di un tipo di eccezione, il parametro catch è implicitamente `final`. Nell'esempio sopra `ex` è marcato `final` e perciò non è possibile assegnare alcun valore ad esso all'interno del blocco catch.


### The `finally` Block








## Basic I/O

## Concurrency

## Networking
