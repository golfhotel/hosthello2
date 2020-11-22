---
title:      Note di programmazione base
layout: 	post
date:   	2017-05-27
author: 	Ivan
categories: [linguaggio c]
summary:    
featured:
  show: false
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1515879218367-8466d910aaa4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70"
  image_alt: "Sono l'alt dell'immagine"
  image_title: "Sono il title dell'immagine"
sidebar: false
#  - trujillo: false
#    related_posts: true
---

Alune note utili per affrontare l'esame di programmazione 1 sul lignuaggio `C`.

## Funzioni di string.h

* `char *strcat(char *dest, const char *src);`
	Concatena la stringa src alla stringa dest modificandola. Ritorna la stringa risultante.
	Il carattere ```\0``` della prima stringa è scartato.

* `char *strncat (char *dest, const char *src, size_t n);` 
	Concatena al massimo n caratteri di src alla stringa dest e ritorna la stringa risultato.

* `int strcmp(const char *s1, const char *s2);` 
	Confronta la stringa s1 con s2, ritorna 0 se le due stringhe sono uguali, -1 se s1 < s2, oppure 1 altrimenti (il segno del risultato corrisponde al risultato della differenza tra s1 e s2).

* `int strncmp (const char *, const char *, size_t);` 
	Confronta al massimo n caratteri delle due stringhe.

* `char *strcpy(char *s1, const char *s2);`
	Copia la stringa s2 nella stringa s1, incluso il carattere di terminazione `'\0'`.

* `char *strncpy(char *s1, const char *s2, size_t n);` 
	Copia al massimo n caratteri della stringa s2 nella stringa s1.

* `size_t strlen(const char *s);` 
	Restituisce la lunghezza della stringa s.

## Allocare memoria con `malloc()`.

La memoria del calcolatore è divisa in sezioni.

```c
+-------------------+
|       Stack       |  ----> per le variabili a spazio fisso
+-------------------+
|        Heap       |  ----> per le variabili a spazio dinamico
+-------------------+
|       Codice      | -----> dove risiede il programma da eseguire
+-------------------+
```

* **Stack**: è la zona di memoria usata per le **variabili locali** che non necessitano di spazio in più in fase di esecuzione del programma. Ricorda: ogni volta che una variabile locale (una variabile **interna** ad una funzione) viene dichiarata, le si alloca una zona di memoria. Questa allocazione avviene nella memoria Stack. Quando la funzione termina, termina anche la "vita" della variabile che in automatico viene deallocata dalla memoria Stack (in pratica la memoria viene liberata).

* **Heap**: è la memoria che un programma può usare per le variabili locali allocabili in fase di esecuzione del programma (**runtime**). È una memoria dinamica che aumenta e diminuisce a secondo delle necessità del programma stesso. **Non** viene deallocata automaticamente; deve essere il programma a farlo in modo esplicito. 

La funzione `malloc()` permette di usare la memoria **heap**. `Malloc()` permette di usare esattamente la quantità necessaria per un determinato valore, infatti se le si dice che si ha necessità di memoria per ospitare un numero intero, allocherà una quantità di memoria per un numero intero (ne più, ne meno). La funzione `malloc()` ritorna un **puntatore** al nuovo spazio allocato nella memoria **heap**

Per usare a gunzione `malloc()` bisogna usare la libreria seguente: 

```c
//libreria necessaria per usare malloc()
#include <stdlib.h>
```

Il puntatore che `malloc()` ritorna è un puntatore di tipo `void *`, ossia un puntatore il cui tipo non è intero o float o struttura ecc...

![foo](../img/hero.png "Foo")

Per determinare la quantità di memoria che `malloc()` deve allocare si usa la funzione `sizeof()`. Ad esempio `sizeof(int)` ritorna la dimensione di una variabile intera che in questo caso sarà 16 o 32 bit (in base all'HW della macchina e al Sistema Operativo in uso). 

Sapendo come fare per trovare la dimensione necessaria per una variabile. Possiamo quindi dire a `malloc()` quanta memoria riservare per la variabile stessa. Ad esempio proviamo ad allocare la memoria per una varibile di interi.

```c
#include <stdlib.h>
...
malloc( sizeof(int) );
```

Il codice sopra dice alla memoria heap di riservare una spazio di memoria adatto per *una* variabile intera. 

Abbiamo detto che `malloc()` ritorna l'indirizzo della memoria allocata nello **heap**. Per usare tale indirizzo è necessario dichiarare una variabile puntatore, ossia l'unica variabile capace di gestire indirizzi di memoria. 	

```c
//dichiaro e inizializzo puntatore
int *ptr = (int *) malloc( sizeof(int) );
```

Nel codice dichiariamo un puntatore inizializandolo con l'indirizzo memoria restituito dalla funzione `malloc()`. Viene inoltre fatto il casting con `(int *)` perchè `malloc()` restituisce un puntatore di tipo  `void *`, mentre noi vogliamo un puntatore di tipo `int` (dal momento che la memoria dovrà contenere un dato intero).

**Ricorda.** Casting è un modo usato per far apparire diversamente le variabili. È come travestire le variabili di un certo tipo con le vesti di un'altro tipo.

```c
//esempio di casting
float foo = 10.5;
int bar = (int) foo; //travesto la variabile float come un intero
```

Nella variabile `bar` viene inserito solo il valore `10`, ossia la parte intera. È come se alla variabile `bar` si presentasse il valore `foo` (che è un `float`) travestito da `int`. Senza il casting si avrebbe un errore di compilazione.

## Variabile puntatore di tipo struttura.

Se una variabile puntatore di tipo `struct` non viene allocata con `malloc()`, non è possibile accedere e/o usare gli elementi interni della struttura. 

![alt text](https://images.unsplash.com/photo-1560161694-baab0988dd58?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70 "Logo Title Text 1")

Per chiarire vediamo un esempio: 

```c
struct node_t{
	int value;
	struct node_t *next;
};

struct list_t{
	struct node_t *head;
};

struct list_t *list = (struct list_t *)malloc(sizeof(struct list_t));
```

Considerando per ora solo `*head`, notiamo che è un puntatore, ossia una variabile utilizzata per contenere indirizzi di memoria. Mentre `struct node_t` è il tipo di dato che dovrà essere contenuto all'indirizzo di memoria presente in `*head`.

Il codice sopra chiede alla memoria lo spazio sufficiente per contenere un indirizzo di memoria (il tipo non ha importanza in questo momento): essendo un indirizzo di memoria grande 8 byte (64 bit), la memoria che verrà riservata sarà di 8 byte.

La cosa importante da capire è cheusando il seguente codice si otterrà un errore a **run-time**:

```c
//si ottiene errore a run-time
head->value = 100;
```

Questo perchè non è stato richiesto nessuno spazio per contenere i campi (nel nostro caso `value`) della struttura `struct node_t`. 

Con l'istruzione sotto è stato chiesto uno spazio di 8 byte per contenere un'indirizzo di memoria, e basta! 

```c
struct list_t *list = (struct list_t *)malloc(sizeof(struct list_t));
```

Per poter accere ai campi di `struct node_t` bisogna chiedere esplicitamente la memoria al calcolatore:

```c
struct node_t *node = (struct node_t *)malloc(sizeof(struct node_t));
```

Il codice sopra chiede spazio sufficiente per contenere un valore di tipo `int`, tipicamente grande 4 byte (32 bit) e per contenere un indirizzo di memoria grande 8 byte (64 bit).

Dopo aver allocato tale spazio di memoria sarà possibile accedere agli elementi interni alla variabile puntatore `*node` di tipo `struct node_t` con il seguente codice: 

```c
//assegnazione usando usando node 
node->value = 100; //numero intero
node->next = &foo; //(es.) indirizzo memoria di una variabile chiamata foo

//assegnazione usando usando gli indirizzi di head e poi node 
head->node->value = 100; //numero intero
head->node->next = &foo; //(es.) indirizzo memoria di una variabile chiamata foo
```


## Puntatori VS ```&```

**Come funziona ```&``` con le variabili.** Il codice ```&``` restituisce l'indirizzo di memoria della variabile, ossia l'indirizzo fisico della memoria dove la variabile risiede.

```c
int a = 0; 
printf( "Indirizzo memoria di a: %p", &a );

//esempio di output
Indirizzo memoria di a: 0x10000020
```

**Come funziona ```&``` con gli array?** Passare il nome dell'array è come passare l'indirizzo del primo elemento dell'array. L'indirizzo del primo elemento dell'array si identifica così ```&array[0]```.

```c
int array[5];
printf( "Indirizzo memoria di array: %p", array );
printf( "Indirizzo memoria di array: %p", &array[0] );
```
Quindi usare ```array``` o usare ```&array[0]``` è la stessa cosa. 

**Come funziona ```&``` con i puntatori?** Una variabile puntatore contiene l'indirizzo fisici di variabili il cui contenuto può essere un intero, float ecc... Quindi se vediamo il contenuto della variabile cui punta il puntatore, troveremo per esempio un numero intero. L'indirizzo fisico si assegna al puntatore nel seguente modo.

```c
// assegno al puntatore ptr l'indirizzo della variabile a
int a = 0;
int * ptr = &a; 

printf( "Indirizzo memoria di a: %p", &a );
printf( "Ptr contiene l'indirizzo di a: %p", ptr );
printf( "Contenuto variabile a accessibile tramite ptr: %i", *ptr );
```

**Come lavora ```&``` con i doppi puntatori?** Un doppio puntatore si comporta allo stesso modo di un puntatore "singolo". Contiene sempre indirizzi fisici ma questa volta l'indirizzo fisico è l'indirizzo di un altro puntatore. Quindi se andiamo a vedere il contenuto della variabile a cui punta il puntatore, troveremo non più un valore intero, ma un indirizzo fisico.

```c
// assegno al puntatore ptr l'indirizzo della variabile a
int a = 10;
int *  ptr  = &a; 
int ** ptrd = &ptr; 

printf( "\nValore variabile a:        %i", a );
printf( "\nIndirizzo memoria di a:    %p", &a );

printf( "\n\nValore variabile ptr:    %p", ptr );
printf( "\nIndirizzo memoria di ptr:  %p", &ptr );
printf( "\nValore cui punta ptr:      %i ", *ptr );

printf( "\n\nValore variabile ptrd:   %p", ptrd );	
printf( "\nIndirizzo memoria di ptrd: %p", &ptrd );
printf( "\nValore cui punta ptrd:     %i", **ptrd );
printf("\n\n");

//output
Valore variabile a:        10
Indirizzo memoria di a:    0x7ffc9fe950a4

Valore variabile ptr:      0x7ffc9fe950a4
Indirizzo memoria di ptr:  0x7ffc9fe950a8
Valore cui punta ptr:      10

Valore variabile ptrd:     0x7ffc9fe950a8
Indirizzo memoria di ptrd: 0x7ffc9fe950b0
Valore a cui punta ptrd:   10

```

## Puntatori e doppi puntatori passati a funzioni

Un puntatore passato ad una funzione equivale passare alla funzione un indirizzo fisico, ossia l'indirizzo fisico della variabile presente nel puntatore.

