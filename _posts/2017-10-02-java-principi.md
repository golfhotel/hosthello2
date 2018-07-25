---
title: Note di Java.
summary: Informazioni e note sul linguaggio Java.
seo: 
  title: 
  summary: foo bar baz
---

Stralci informativi sulla programmazione e sul linguaggio Java, utili per chi vuole riprendere i concetti più importanti. Per approfondimenti sulla materia è riportato in calce il testo di riferimento. 

>La programmazione è un processo creativo.

---

## Per iniziare

Alcune caratteristiche del linguaggio Java.

### Invocare un metodo.

In un programma Java, un oggetto esegue un'**azione** quando si invoca un suo metodo. 

Si usano quindi oggetti per eseguire azioni. Le azioni sono identificate nei metodi.

```java
// oggetto
System.out ...
```

```java
// oggetto con metodo println
System.out.println("Foo");
```

L'azione è quella di stampare a video la stringa **Foo**.

```java
// tastiera è un oggetto, nextInt il metodo
tastiera.nextInt(); 
```

### Scrivere, compilare ed eseguire programmi Java

Un programma Java è composto da una o più classi. Una classe può essere scritta usando un editor di testi. La classe si salva usando come nome lo stesso nomo della classe. Per eseguire il programma Java, bisogna compilarlo usando il comando ```javac```.

```java
javac MiaClasse.java
```

Con la compilazione si crea un file con estensione ```.class```. Questo file è la traduzione del codice Java in codice eseguibile dalla JVM.

```java
// a seguito della compilazione si ottiene
MiaClasse.class
```

Per eseguire il programma Java si usa il comando ```java [nome classe intero programma]```.

```java
//esecuzione programma
java MiaClasse
```

### Oggetti, metodi e classi

Un oggetto ha diverse caratteristiche chiamate **attributi**.

Gli attibuti dell'oggetto autmobile sono: 

* nome
* velocità corrente
* livello carburante 
* ecc...

I valori di tali attribbuti (es. Ferrari California, 200 km/h, 50 litri) costituiscono lo **stato** dell'oggetto. 

Le azioni che un oggetto può effettuare sono dette **comportamenti**, chiamati anche ***metodi*** dell'oggetto.

Una classe definisce il tipo di dato di un oggetto.

### OOP - Programmazione orientata agli oggetti

OOP è una metodologia di programmazione che definisce oggetti i cui comportamenti e le interazioni permettono di raggiungere un certo risultato. La programmazione orientata agli oggetti adotta i seguenti 3 principi fondamentali di progettazione: 

* **inapsulamento**: gli oggetti è come se fossero chiusi in una capsula accessibile dall'esterno per scopi di uso. I dettagli del contenuto della capsula sono informazioni nascoste a chi usa l'oggetto.

* **polimorfismo**: un'istruzione di un programma può significati e forme diverse in vari contesti. Esempio la pressione del tasto ON di un pc, spazzolino elettrico o iPod, rispondono tutti in modo differente, ma approprioato. In Java il nome di un metodo, usato come istruzione, può causare azioni differente a seconda degli oggetti che svolgono l'azione.

* **ereditarietà**: ossia il modo di organizzare le classi. Una sorta di gerarchia che consente di ereditare proprietà comuni ad altre classi. Permette di evitare che il programmatore ripeta istruzioni per ogni singola classe.

### Algoritmo 

Insieme di direttive usate per risolvere un determinato problema. Le direttive devono essere espresse in modo completo e preciso. 

**Pseudocodice.** Mix di linguaggio naturale (es. italiano) e linguaggio Java. L'algoritmo è scritto in pseudocodice. L'italiano e Java si alternano in base alla comodità di espressione. 

---

## Convenzioni

* Inizializzare sempre le variabili
 
```java 
int somma = 0 
 ```

* Costanti. Si nominano usando il maiuscolo. I nomi composti si creano usando l'underscore. Prima della dichiarazione variabile inserire ```public static final```. 

```java
public static final int GIORNI_PER_SETTIMANA = 7;
```

È sconsigliato usare gli **operatori di incremente e decemente** nelle espressioni.

```java
int n = 3; 
int m = 4;
int risultato = n * (++m);
```


## Compatibilità di assegnamento 

Un valore può essere assegnato a una qualsiasi variabile il cui *tipo* compare alla destra del tipo del valore nel seguente elenco: 

```
byte → short → int → long → float → double 
```

Un valore di tipo intero lo si può assegnare a qualsiasi variabile di tipo virgola mobile. Diversamente un valore di tipo ```double``` (es. 3.5) non può essere asseganto a una variabile di tipo ```int```.

È possibile anche inserire un valore di tipo ```char``` a una variabile ```int``` o a qualsiasi tipo numerico più a destra di ```int```, come nel seguente elenco.

```
char → int → long → float → double 
```

## Conversione di tipo

Per memorizzare un valore ```double``` in una variabile ```int``` è necessario eseguire una conversione (type cast).

```java
//esempio di type cast
double supposizione = 7.8;
int risposta = (int)supposizione;
```

Nella varibile ```risposta``` sarà memorizzato il numero ```7```.

### Convertire char in int

```java
char simbolo = '7';
System.out.println((int)simbolo);
```

Produce l'output con valore intero ```77```.


