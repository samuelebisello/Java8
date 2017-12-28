# Java 8

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

* **Parametri**

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

**NB**: Per variabili locali il compilatore non assegna mai un valore di default, perciò prima di
usarle ricordati sempre di inizilizzarle. Accedere ad una variabile locale non inizializzata
produce un errore di compilazione.

### Classes

### Declaring Classes

Dichiarazione di una classe

```java
class MyClass {
  // campi dati, costruttore, dichiarazione metodi
}

class MyClass extends MySuperClass implements YourInterface {
  // campi dati, costruttore, dichiarazione metodi
}
```

### Methods

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
possono avere lo stesso nome se hanno una differente lista di parametri.

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

### Creating Objects

```java
Point MyPoint = new Point(23,94);
```
Questo statement è costituito da tre parti:

* **Dichiarazione**
* **Instanziazione**
* **Inizializzazione**

#### #Dichiarazione

Una dichiarazione associa un nome di variabile con un tipo di oggetto.

`type name`

Questo notifica al compilatoreche userai `name` per riferirti ad un oggetto che ha tipo `type`.
Il valore di name sarà indeterminato fino a quando un oggetto sarà effetivamente creato e
assegnato  ad esso. Dichiarare un varibile riferimento non crea un oggetto.



#### #Instanziazione

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

#### #Inizializzazione

L'operatore `new` è seguito da una chiamata al construttore il quale inizializza il nuovo
oggetto.

#### Garbage Collector

Un oggetto è eleggibile per il garabage collector quando non è più riferito da alcuna variabile.


#### This Keyword

In un metdodo di istanza o in un costruttore `this` è un riferimento all'oggetto corrente, ossia
l'oggeto su cui viene chiamato il metodo o il costruttore.

All'interno di un costruttore si può usare la keyword `this` per chiamare un altro costruttore
nella stessa classe. Si tratta di una chiamata esplicita al costruttore.


#### Control Access to Members of a Classe

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


#### Acces Levels

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

##### Tips on Choosing an Acces Level

Usa il modificatore di accesso più restrittivo che abbia senso per un particolare membro.
* Usa`private` a meno che non ci sia un buon motivo per non farlo.
* Evita i campi `public` eccetto che per le costanti.

I campi marcati `public` tendono a vincolarti ad una particolare implementazione e limitare la
in flessibilità nel modificare il codice.

#### Class Variables [static]

Campi dati dichiarati `static` sono chiamati campi dati statici o variabili di classe.
Sono associati alla classe invece che ad un oggetto. Ogni istanza di una classe condivide una
variabile di classe, la quale si trova in una regione fissa di memoria. Ogni oggetto può
cambirare il valore di una variabile di classe, ma le variabile di classe possono essere
manipolate anche senza creare un istanza di quella classe.

Le variabili di classe sono referenziate dal nome della classe:

```java
ClassName.staticVariable;
```

#### Class Methods

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

#### Constants

Il modificatore `static` in combinazione a `final`, viene spesso usato per definire costanti.
Il modificatore `final` indica che il valore di quel campo **non** può cambiare.

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

#### Static Initialization Blocks

un blocco di inizializzazione statica è un normale blocco di codice racchiuso tra due `{ ... }`.


```java
static {
  // code here fot init...
}
```

Una classe può avere qualsiasi numero di blocchi di inzializzazione statico, e possono apparire
in qualsiasi punto del corpo della classe. Il sistema a runtime garantisce che i blocchi di
inizializzazione statica sono chiamati nell'ordine in cui appaiono nel codice.


#### Initializing Instance Members

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
è utile solo per un altra classe, allora è logico integrarla nell'altra classee tenerle insieme.

* Aumenta l'ncapsulamento: Supponiamo due classi di primo livello A e B. Se B ha bisogno di accedere ai membri di A devono essere dichiarati pubblici. Nascondendo la classe B all'interno di A i membri di A possono essere dichiarati privati e B può accedervi. Inoltre B è nascosta dal mondo esterno.

* Può portare a un codice più leggibile e gestibile: L'inserimento di classi di piccole dimensioni all'interno di una classe di alto livello avvicina il codice a dove viene utilizzato.

#### Inner Class

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

#### Shadowing

Se una dichiarazione di un tipo (come una variabile membro o un nome di un parametro) in un particolare scope (come in una classe interna o nella definizione di un metodo) ha lo stesso nome di un'altra dichiarazione di variabile in uno scope più esterno, allora la dichiarazione nello scope più interno nasconde quello nello scope più esterno.


#### Local Class
