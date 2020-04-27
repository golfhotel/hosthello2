---
title: Come gestire le stringhe con getchar
title_in_home: Gestire le stringhe con getchar
date: 2016-08-22 12:00:00
layout: post
summary: Aquisita una stringa digitata dall'utente, verrà controllata per determina se contiene al massimo due caratteri uguali di seguito.
featured: 
  show: yes
---

Tramite un esempio vedremo come gestire le stringhe usando la funzione `getchar()` della libreria `stdio.h`. Aquisita una stringa digitata dall'utente, verrà controllata per determina se contiene al massimo due caratteri uguali di seguito. 

```c
#include <stdio.h>
#include <stdbool.h>

// dichiarazione prototipo funzione
bool al_massimo_due_di_seguito_(const char *s);

int main (void){
    char character = 0;
    char string[81]; // 81 è il numero max di caratteri inseribili da console
    int i = 0;
    
    printf("\n**************************************\n"
    "Verifico se in una parola ci sono \n"
    "al max 2 caratteri uguali consecutivi.\n"
    "**************************************\n\n"
    "Inserisci una parola: ");
    
    // riempimento array con caratteri 
    do{
        character = getchar(); // leggo carattere per carattere da tastiera
        string[i] = character; // ogni carattere è inserito in un array
        i++;
    }while( character != '\n' );
    
    //l'array di char diventa una stringa a tutti gli effetti
    string[i - 1] = '\0';

    // stampa output integrando dati da una funzione
    printf("\n> Ci sono %s caratteri uguali consecutivi! \n\n", 
    al_massimo_due_di_seguito_(string) ? "da 0 a 2" : "più di 2");
    
    return 0; 
}

// funzione di conteggio caratteri uguali 
bool al_massimo_due_di_seguito_(const char *s){
    while ( *s ){
        if ( *s == *(s + 1) && *s == *(s + 2) ) 
            return false;
            
        s++;
    }

    return true;
}
```


Un esempio di output:

```c
**************************************
Verifico se in una parola ci sono 
al max 2 caratteri uguali consecutivi.
**************************************

Inserisci una parola: qwertt

> Ci sono da 0 a 2 caratteri uguali consecutivi! 
```

Altro esempio di output:

```c
**************************************
Verifico se in una parola ci sono 
al max 2 caratteri uguali consecutivi.
**************************************

Inserisci una parola: qweeerty

> Ci sono più di 2 caratteri uguali consecutivi!  
```

### Cosa succede.

Una volta dichiarato e inizializzata la variabile `char character` e l'array `char string[81]`, si chiede all'utente di inserire la stringa da elaborare: 


```c
//riempimento array con caratteri 

do{
    character = getchar(); // leggo carattere per carattere da tastiera
    string[i] = character; // ogni carattere è inserito in un array
    i++;
}while( character != '\n' );
```

Variante senza l'uso della variabile d'appoggio `character`:

```c
//riempimento array con caratteri 

do{
    string[i] = getchar(); // ogni carattere è inserito in un array
    i++;
}while( string[i - 1] != '\n' );
```

Altra variante con l'uso di post incrementento `i++`:

```c
//riempimento array con caratteri 

do{
    string[i] = getchar(); // ogni carattere è inserito in un array
}while( string[i++] != '\n' );
```


La funzione `getchar()`, quando invocata, legge un *buffer* di lettura. Il *buffer* di lettura è una caratteristica del terminale (shell o linea di comando) che immagazzina lo streaming dei caratteri inseriti tramite tastiera. La lettura termina quando viene premuto il tasto `Enter/Invio`, che inserirà `\n` come ultimo carattere del buffer.

> `getchar()` inserisce il carattere `\n` come ultimo elemento del buffer di input. 

Quando `getchar()` è invocato **per la prima volta** può trovare il buffer di lettura in due stati: 

1. **Buffer vuoto**.  In questo caso il buffer di lettura si attiva e si attende che l'utente riempia il buffer con dei caratteri e prema `Enter/Invio` per terminare (è un'operazione che avviene su linea di comando). Una volta terminata l'immmissione caratteri la funzione `getchar()` (sempre nella stessa iterazione) va a leggere il singolo **primo** carattere del *buffer*. Dopo la lettura il carattere letto viene "eliminato dal buffer" e il carattere successivo diventa il primo.

2. **Buffer con elementi.** Se nel buffer di input sono presenti elementi, `getchar()` leggerà il singolo primo carattere del buffer che verrà poi eliminato per essere rimpiazzato dal carattere successivo (come visto prima).

Nel nostro `while` quando si incontra il carattere "a capo" `\n` si esce dal loop. 

Ora, avendo letto il singolo carattere, è necessario conservarlo in modo da ricomporre, poi, l'intera stringa. Con l'uso di un ciclo e di un array riusciamo a leggere il singolo carattere e conservarlo. 

Al termine della lettura caratteri (e quindi quando si incontra `\n`) l'array `char string[]` lo troveremo riempito così (esempio): 

```c
char stringa[] = { q, w, e, r, t, y, \n }
```

**Ricorda.** Una stringa è "considerata" un array di caratteri ma per essere una stringa a tutti gli effetti **deve** terminare con il carattere nullo `\0` o `NUL`. Il carattere nullo `\0` verrà sempre inserito per default dal linguaggio C **solo** se si inizializza un array di `char` nel seguente modo:

```c
//carattere nullo inserito di default

char s[21] = "FooBarBaz";
```

Quando si dichiara l'array di `char` per la stringa, bisogna dimensionarlo in modo da includere "lo spazio" per il carattere `\0`. Noi abbiamo dichiarato l'array `char string[21];` per contenere 21 caratteri, di cui 20 saranno dedicati per il testo tra virgolette e 1 sarà usato per il carattere nullo `\0` . Se si inserisce un testo lungo 21 caratteri si generea un comportamento *inatteso*, ossia possono verificarsi problemi d'uso del programma.

Quindi la stringa creata con l'uso di `getchar()` dovrebbe diventare la seguente:

```c
char stringa[] = { q, w, e, r, t, y, \0 }
```

Per realizzare quanto scritto sopra si usa la seguente istruzione

```c
//l'array di char diventa una stringa a tutti gli effetti

string[i - 1] = '\0';
```

Vediamo poi cosa succede nella parte successiva del codice:

```c
//funzione di conteggio caratteri uguali 

bool al_massimo_due_di_seguito_(const char *s){
    while ( *s ){
        if ( *s == *(s + 1) && *s == *(s + 2) ) 
            return false;
            
        s++; //vado al successivo indirizzo fisico a cui punta s
    }

    return true;
}
```

Quando viene invocata, la funzione sopra prende ***l'indirizzo*** della stringa di caratteri inserita dall'utente e la elabora con l'uso dei puntatori. Inizialmente il puntatore punta all'indirizzo del primo carattere della stringa. Fin quando il *contenuto* a cui punta il puntatore  ```*s ``` è diverso dal carattere nullo  ```\0``` (il carattere nullo equivale a 0), il ciclo ```while``` incrementa la posizione di memoria a cui punta ```*s``` passando quindi al carattere successivo (ogni carattere si trova in una cella di memoria con un proprio indirizzo fisico).  

La parte di codice con l' `if` fa un confronto dei **contenuti** presenti nei relativi ***indirizzi di memoria*** a cui punta `*s`, `*s + 1` e `*s + 2` "ritornandone" `true` o `false` a seconda dei casi. 

**Nota.** L'istruzione `*(s + 1)` è il contenuto posizionato all'indirizzo di memoria successivo ad `s`. Lo schema seguente dovrebbe chiarirne il concetto.

| Puntatore  | Contenuto | Indirizzo memoria |
|-----------:|:---------:|:-----------------:|
| *s =       |  f        | 0x1024            |
| *(s + 1) = |  o        | 0x1025            |
| *(s + 2) = |  o        | 0x1026            |


## Perchè usare il carattere nullo 

Come anticipato, una stringa è tale se è un array di caratteri che termina con il carattere nullo `\0` o `NUL`. **Attenzione** che `NUL` è diverso da `NULL`, infatti il primo equivale a `0` nella tabella ascii, mentre il secondo è usato con riferimento ai puntatori. 

Usare il carattere nullo in un array di `char` è richiesto prima di tutto per questioni di "grammatica" del linguaggio C e poi perchè molte funzioni che lavorano con le stringhe necessitano del carattere nullo per lavorare correttamente. 

> Un array di char (caratteri) è una stringa a tutti gli effetti solo se termina con il carattere nullo! Diversamente è solo un array contenente caratteri.

Quindi, un array di `char` che non termina con un carattere nullo, non è considerato una stringa a tutti gli effetti.

## Variante con i puntatori

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>

int main (void){
    char character;
    //alloco spazio per 256 char
    char *str = (char *) malloc( 256 * sizeof(char)); 
    char *strHead = str;

    printf("\n> Scrivi del testo: ");
    // riempimento spazio con caratteri 
    do    
         *str++ = getchar(); // ogni carattere è inserito in una locazione di memoria        
    while( *(str - 1) != '\n' );

    *(str - 1) = '\0'; //termino immissione con carattere nullo 

    printf("\n> Hai scritto \"%s\".\n\n", strHead );
    
    free(strHead);
    
    return 0;   
}

```

## Bibliografia o altri riferimenti

* [What is the standard input buffer?](http://stackoverflow.com/questions/14068346/what-is-the-standard-input-buffer){:target="_blank"}
* [Input da tastiera](http://www.repni.it/view/guida_c_base_input_da_tastiera.html){:target="_blank"}
* [Standard input (stdin)](https://it.wikipedia.org/wiki/Canali_standard#Standard_input_.28stdin.29){:target="_blank"}
