---
title: Variabile constante e scanf()
date: 2016-08-24 12:00:00
layout: post
author: Ivan Garrini
category: [linguaggio c]
summary: Un tipico esempio di come la compilzione non è sempre efficace per prevenire errori. Usando scanf() andremo a capire meglio la problematica.
featured:
  image: 
  image_from_url: "https://images.unsplash.com/photo-1539186607619-df476afe6ff1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70"
---

**Esempio 1.** Il codice seguente dichiara e "inizializza" la variabile intera number con il valore 42. La parola `const` (che tecnicamente si chiama **qualificatore**) serve per dire al compilatore che la variabile avrà un valore costante durante l'esecuzione del programma. 

```c
#include <stdio.h>

int main(void){
    const int number = 42;
        
    printf("number = %i", number);
    
    return 0;
}
```

Con l'esecuzione del programma otterremo il seguente output:

```
number = 42 
```

Ora proviamo a modificare il valore di number  con ```number = number / 2; ```:

```c
#include <stdio.h>

int main(void){
    const int number = 42;
    number = number / 2;    // modifica di number
        
    printf("number = %i", number);
    
    return 0;
}
```

Con gcc la compilazione non andrà a buon fine (non avremo il programma eseguibile), ottenendo il seguente messaggio: 

```
**error: assignmernt of read-only variable 'number'**.
```

Questo fa capire che il compilatore non vuole che esista una parte di codice del programma capace di modificare la varibile `number`. Il compilaotre vuole che lo "slot di memoria" (all'interno dello STACK) della variabile `number` mantenga un valore *costante* per l'intera esecuzione del programma.

**Esempio 2.** Ora vediamo un esempio simile a quello precedente dove la modifica della variabile non viene fatta "in-line" da una parte di codice del programma, ma viene eseguita durante l'esecuzione del programma tramite la funzione ```scanf();```

```c
#include <stdio.h>

int main(void){
    const int number = 42;
        
    printf("number = %i \n", number);
    
    printf("Digita un numero: ");
    scanf(" %i", &number);
    printf("number = %i \n", number);
    
    return 0;
}
```

Con gcc la compilazione andrà a buon fine (avremo il programma eseguibile) ma il compilatore ci avverte con il seguente messaggio: 

```
**warning: writing into constant object**.
```

Questo **warning**, ci informa che la costante potrebbe subire modiche da un'altra funzione.

Eseguendo il programma, verrà chiesto all'utente di digitare un numero. Noteremo che la varibile  ```number ``` subirà un cambio valore (il valore sarà quello digitato dall'utente). 

Un esempio di output:
 
```
number = 42 
Digita un numero: 30
number = 30 
```

Ma come è possibile se la varibile è stata dichiarata come costante e non dovrebbe subire modifiche essendo "di sola lettura"?

Nell'esempio 1 la modifica "in-line" del codice e la successiva compilazione,  fanno capire al compilatore la **"volontà"** di voler cambiare il valore di una costante. Di conseguenza il compilatore genera un messaggio di errore e non crea il programma eseguibile. 

Nell'esempio 2 la modifica della variabile tramite l'uso di ```scanf(" %i", &number);``` non interesserà il compilatore perchè il programma viene comunque compilato. In poche parole il compilatore nota che scanf() andrà a modificare una costante ma non ne vieta la modifica. 

Quindi, durante l'esecuzione del programma, è possibile riassegnare un nuovo valore ad una costante! Questo perchè una variabile, costante o no, è sempre una locazione di memoria sullo STACK e la regola della "costanza" può essere infranta semplicemente sovrascrivendo la locazione di memoria. 

Tale uso e metodo comporta ovvi problemi di comportamenti imprevisti del programma stesso.


### Bibliografia o altri riferimenti

* [Can we change the value of a constant through pointers?](http://stackoverflow.com/questions/3801557/can-we-change-the-value-of-a-constant-through-pointers)
