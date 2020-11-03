---
title: 		Puntatori e variabili
layout: 	post
date:   	2017-05-27
author: Ivan Garrini
summary: I puntatori sono la base per capire come nella programmazione è usata la memoria.
categories: [linguaggio c]
featured:
  show: false
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1597848007618-54db4e82fe3a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70"
  image_alt: "Sono l'alt dell'immagine"
  image_title: "Sono il title dell'immagine"
sidebar: false 
latest_posts:   yes
---

Un puntatore è come una normale variabile ma con un "potere" in più. Esso infatti non contiene dati in modo esplicito, ma **contiene l'indirizzo di memoria** di un'altra variabile. 

>Il puntatore è una variabile di tipo indirizzo, ossia che contiene un indirizzo di memoria del calcolatore.

Essendo il puntatore una variabile va dichiarato allo stesso modo delle altre variabili. 

```c
// dichiarazione puntatore
// il puntatore può contenere solo indirizzi memoria
int *ptr; 
```

L'asterisco identifica che la variabile `ptr` è un puntatore ossia una variabile capace di gestire valori **alfanumerici** come gli indirizzi di memoria (es. 0x001001001028). 

> Un variabile dichiarata come puntatore è l'unico elemento che può contenere un dato alfanumero e gestirlo come tale senza alterarne il significato.

In questo caso la variabile è un puntatore ad `int`: ciò significa che il contenuto gestibile da questa variabile puntatore dovrà essere un indirizzo di una **cella di memoria** del calcolatore il cui contenuto sia un numero intero. Considerando che ci sono 3 protagonisti (la variabile puntatore, la variabile intera, il contenuto della varibile intera) il concetto sarà più chiaro avanti.

Una volta dichiarato, è possibile maneggiare la variabile puntatore senza dover usare l'asterisco. Ma in alcuni casi vedremo che l'`*` è necessario.

> Dichiarare una variabile vuol dire **assegnare** un indirizzo di memoria alla variabile.

In questo momento il puntatore è stato dichiarato ma non inizializzato. Proviamo a vedere cosa contiene: 

```c
// dichiarazione puntatore (ma non inizializzato)
int *ptr;

// stampo valore del puntatore
printf("ptr = %p\n", ptr);

//output
ptr = (nil) // oppure 0x7ffe71335ea0 (indirizzo a caso)
```

Il contenuto di un **puntatore non inizializzato** dipende dalla macchina e **non è** sempre lo stesso. Dato che un puntatore deve contenere indirizzi di memoria (diversamente sarebbe una normale variabile), se non inizializzato potrebbe contenere quanto segue:

* contenuto `(nil)`: identifica che il puntatore non contiene nessun indirizzo di memoria

* contenuto `0x7ffe71335ea0`: un indirizzo di memoria **scelto a caso dall'elaboratore**. 

```
       Memoria calcolatore   Indirizzi di memoria
      +-------------------+  ↑
      │         ...       │ ... 
      +-------------------+       
      │         ...       │ ...
      +-------------------+       
      │         ...       │ ...
      +-------------------+       
 ptr  │       (nil)       │ 0x001001001024
      +-------------------+        

// oppure

       Memoria calcolatore    
      +-------------------+       
      │         ...       │ 0x7ffe71335ea0
      +-------------------+   
      │         ...       │   
      +-------------------+       
      │         ...       │   
      +-------------------+
 ptr  │   0x7ffe71335ea0  │ 0x001001001024
      +-------------------+       
```

Per identificare l'indirizzo memoria di una variabile si usa il carattere `&` seguito dal nome variabile. Infatti se dichiariamo una varibile `var` e vogliamo stamparne l'indirizzo di memoria (o indirizzo fisico) possiamo fare così:

```c
// dichiarazione variabile
int var; 

// stampo indirizzo memoria variabile
printf("&var = %p", &var);

// output d'esempio: indirizzo memoria di var
0x001001001028
```

Ora, il puntatore per essere utile deve **contenere** (in gergo puntare) un indirizzo di memoria di un'altra variabile. Come una normale variabile intera contiene un numero intero, un puntatore deve contenere un indirizzo di memoria. L'indirizzo di memoria non è un elemento "amichevole" da trovare per l'uomo, quindi per identificarlo si dichiara prima una variabile (ricordiamo che dichiarare una variabile vuol dire assegnare alla variabile una locazione della memoria, per cui un indirizzo di memoria) e poi si assegna l'indirizzo della variabile al puntatore (sappiamo già che l'indirizzo di una variabile si ottine con `&nomevar`). 

```c
//dichiarazione e inizializzazione variabile 
int var = 100;

//dichiarazione puntatore
int *ptr;

//inizializzo puntatore assegnando l'indirizzo memoria della variabile var
ptr = &var;
```

Si può dichiarare e inizializzare in un'unica riga. 

```c
//dichiarazione e inizializzazione puntatore
int *ptr = &var;
```

Cosa succede nella memoria del calcolatore.

```
       Memoria calcolatore    
      +-------------------+       
      │         ...       │ 0x7ffe71335ea0
      +-------------------+      
      │         ...       │
      +-------------------+  
      │   0x001001001024  │
      │         ↓         │
      │ +---------------+ │
      │ │      100      │ │
 ptr  │ +---------------+ │ 0x001001001028
      +-------------------+  
 var  │        100        │ 0x001001001024
      +-------------------+
```

Ora la variabile `ptr` **"punta"** (contiene l'indirizzo) alla variabile `var`. Questo vuol dire che usando la variabile puntatore `ptr` posso accedere al contenuto della variabile `var`. Qualsiasi modifica fatta "tramite" il puntatore è come se venisse fatta alla variabile `var`. 

## Accedere al contenuto della variabile `var` tramite puntatore `ptr`.

Agire "tramite puntatore" non vuol dire "modificare il puntatore". Questo concetto è importante e va capito bene. Vediamo di cosa si tratta.

Per modificare il valore di `var` **tramite** il puntatore devo usare l'asterisco `*` prima del nome variabile puntatore.

```c
// modifico var tramite il puntatore ptr
*ptr = 200;
```

Il codice sopra modifica il valore contenuto nella variabile `var`.

Se **non** si usa l'asterisco si modifica il contenuto della variabile `ptr` che sappiamo deve essere un indirizzo memoria. Per cui è **sbagliato** fare come segue per modificare il valore contenuto nella variabile `var`.

```c
//errato: così non si modifica il valore di var
ptr = 200;
```

Il codice sopra modifica il **contenuto** della variabile `ptr` che (essendo un puntatore) deve contenere **indirizzi di memoria** (che sappiamo dargli usando `&var`) e non valori interi, con virgola ecc...

Al puntatore `ptr` possiamo assegnare un altro indirizzo di memoria di un'altra variabile. 

```c
//dichiaro e inizializzo variabile
int var2 = 200;

//cambio variabile puntata
ptr = &var2
```

## Codice di esempio

```c
#include <stdio.h>

int main(int argc, char const *argv[])
{
	//dichiarazione e inizializzazione variabile 
	int var = 100;

	//dichiarazione puntatore
	int *ptr;

	//inizializzo puntatore assegnando l'indirizzo memoria della variabile var
	ptr = &var;
	
	printf("\nValore contenuto in var\n");
	printf(" var = %i\n\n", var);
	
	printf("Valore contenuto in ptr\n");
	printf(" ptr = %p (indirizzo memoria di var)\n\n", ptr);

	printf("Indirizzo memoria di var\n"); 
	printf("&var = %p\n\n", &var);

	printf("Indirizzo memoria di ptr\n"); 
	printf("&ptr = %p\n\n", &ptr);

	printf("Contenuto puntato da ptr (valore contenuto in var)\n"); 
	printf("*ptr = %i\n\n", *ptr);

	// dichiaro e inizializzo var2
	int var2 = 200; 

	//al puntatore assegno l'indirizzo memoria della variabile var2
	ptr = &var2;

	printf("\nValore contenuto in var2\n");
	printf(" var2 = %i\n\n", var2);
	
	printf("Valore contenuto in ptr\n");
	printf(" ptr = %p (indirizzo memoria di var2)\n\n", ptr);

	printf("Indirizzo memoria di var2\n"); 
	printf("&var2 = %p\n\n", &var2);

	printf("Indirizzo memoria di ptr\n"); 
	printf("&ptr = %p\n\n", &ptr);

	printf("Contenuto puntato da ptr (valore contenuto in var2)\n"); 
	printf("*ptr = %i\n\n", *ptr);	
}
```