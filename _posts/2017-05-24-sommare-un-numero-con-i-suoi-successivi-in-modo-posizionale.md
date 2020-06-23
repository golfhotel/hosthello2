---
title: Sommare un numero con i suoi successivi in modo posizionale.
layout:     post
date:       2017-09-19
author:     Mr. Jim
categories: [html, enviroment, linguaggio c]
summary:  "Ora, conosco la somma totale dei numeri in posizione pari. Se scansiono l’array andando con l’indice solo sui numeri pari, posso trovare la uipse loremaaaa"
# Permalink:
add_to_top_menu:    no
add_to_bottom_menu: no
section:
  blackquote:   Sviluppare progetti web con le tecnologie più potenti è la base di un prodotto vincente e duraturo 
  cite:         Foo Barbaz
  link:         www.google.it
seo:
  title:        This is SEO title
  keywords:     uno, due, tre
# sitemap:
#   exclude: yes
latest_posts:   yes
featured: 
  show: yes
  image_from_url: "https://images.unsplash.com/photo-1588595189116-6e5c7ecc9e86?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1649&q=80"
---

Per ogni numero in un array di interi, 

* se il numero è nella posizione corrente **dispari** dovrà essere sommato con i suoi **successivi in posizione dispari**.
* se il numero è nella posizione corrente **pari** dovrà essere sommato con i suoi **successivi in posizione pari**

```
        ┌ posizione pari
        │  ┌ posizione dispari
        │  │  ... 
arrayA {1, 2, 3, 4, 5 }; //array iniziale
arrayA {9, 6, 8, 4, 5 }; //array finale
        │  │  │  │  │
        │  │  │  │  └ = 5
        │  │  │  └ = 4
        │  │  └ = 3 + 5 = 8
        │  └ = 2 + 4 = 6
        └ = 1 + 3 + 5 = 9
```

## Strategia

Per poter realizzare quanto sopra, si adotta la seguente strategia: 

### Numeri pari

Prendo ogni numero in posizione pari e lo sommo. Conservo la somma.  

```
sommaPari = 1 + 3 + 5 = 9
```

Ora, conosco la somma **totale** dei numeri in posizione pari. Se scansiono l'array andando con l'indice solo sui numeri pari, posso trovare **la somma degli elementi successivi al numero in posizione corrente** così: tolgo dalla somma **totale** i numeri **precendenti** all'elemento in *posizione corrente* (per numero in *posizione corrente* si intende il numero su cui mi trovo con l'indice array).

**Ricorda.** Lo zero è considerato un numero pari ([fonte](https://it.wikipedia.org/wiki/Parit%C3%A0_dello_zero "Parità dello zero")).

```
// 1^ iterazione. Sono stati omessi i numeri dispari.

        ┌ nCorrente[i]
        │  
arrayA {1, -, 3, -, 5 }; //array iniziale
arrayA {9, -, 3, -, 5 }; //array finale
        │     │
        │     └ a fine iterazione sarà il prossimo nCorrente[i]
        └ sommaSuccessiviCorrente
```
`sommaSuccessiviCorrente` = `sommaPari` - `nCorrente[i-2]`

`9` ← `9` - `0`

**Nota.** Guarda di seguito il perchè di `nCorrente[i-2]`.

```
// 2^ iterazione. Sono stati omessi i numeri dispari.

        ┌ nCorrente[i-2]
        │     ┌ nCorrente[i]
        │     │  
arrayA {1, -, 3, -, 5 }; //array iniziale
arrayA {9, -, 8, -, 5 }; //array finale
              │     │
              │     └ a fine iterazione sarà il prossimo nCorrente[i]
              └ sommaSuccessiviCorrente      
```

`sommaSuccessiviCorrente` = `sommaPari` - `nCorrente[i-2]` 

`8` ← `9` - `1`

**Nota.** `nCorrente[i-2]` perchè **non** si vuole il numero successivo (che in questo caso sarebbe dispari), ma il numero di due posizioni avanti.

#### L'ultimo elmento dei pari rimane invariato

Se i numeri pari sono `n`, sipossono svolgere `n - 1` iterazioni: quindi l'ultimo elemento rimane invariato. In termini di prestazioni ha poco senso perchè comunque si tratta di una sola iterazione. Ciò è fattibile agendo sull'indice dell'array. 

### Numeri dispari

Per i numeri dispari si fa la stessa cosa. Ma bisogna ricordare che nella prima iterazione l'indice del **numero corrente** sarà posizionato sul secondo elemento dell'array.

## Codice

Segue la funzione che esegue somma degli elementi successvi a quello corrente.

```
/**
 * PER OGNI NUMERO IN POSIZIONE DISPARI, SOMMALO CON I SUOI SUCCESSIVI
 * DISPARI. INFINE STAMPARE LA SOMMA DI OGNI NUMERO. 
 * STESSA COSA PER I NUMERI DI POSIZIONE PARI.
 * 
 * Es:  
 * arrayA {1, 2, 3, 4, 5 }; //array prima della trasformazione
 * arrayA {9, 6, 8, 4, 5 }; //array dopo la trasformazione
 * 
 * 1+3+5 = 9;
 *   2+4 = 6;
 * ecc..
 *      
*/
#include <stdio.h>

/* dichiarazione prototipo funzioni */
void fillArray( int * , int );
void somma_in_array( int * , int );
int n_elementi();

/* funz. principale */
int main( void ){
    // chiedo dimensione per array
    int lung = n_elementi();

    int array[lung];
    int *ptrArray = array; //genero un puntatore ad un array
    
    //chiamo funzione che riempie array con dati interi e restituisce lunghezza array.
    fillArray( ptrArray, lung );

    // stampo array originale (prima dell'elaborazione)
    int i;
    printf("arrayOriginale { ");
    for( i = 0; i < lung; i++ ){
        printf( "%d ", array[i] );
    }
    printf("}\n");

    
    // chiamo funzione per trasformare array
    somma_in_array( ptrArray, lung );
    
    // stampo array originale (prima dell'elaborazione)
    printf("arrayFinale    { ");
    for( i = 0; i < lung; i++ ){
        printf( "%d ", array[i] );
    }
    printf("}\n\n");
    
    return 0;
}

/* funzione chiede quantità valori */
int n_elementi(){
    int n;
    printf("Quanti valori vuoi inserire? ");
    scanf("%i", &n);

    return n;
}

/* funzione riempimento array con numeri inseriti dall'utente */
void fillArray( int *array_ptr, int n ){
    int i, value;     
    
    // chiedo inserimento valori
    printf( "\nInserisci %i valori. \n", n );
    for( i = 0; i < n; i++ ){
        printf( "Valore #%i: ", i + 1 );
        scanf( "%i", &value );    
        array_ptr[i] = value;
    }
    printf( "\n" );
    
}

/**
 * Funzione di somma elementi successivi al corrente
 *
 * @param *array_ptr: array di tipo puntatore
 * @param n: dimensione array
 * 
 * @return void
 *
*/
void somma_in_array( int *current, int n ){    
    int i, k, j; 

    // Array temporaneo stessa dimensione dell'originale. 
    // usato per non compromettere l'originale. 
    // Conterrà le somme per posizione pari/dispari del numero corrente.
    
    int temp[n];
    for( i = 0; i < n; i++ ){ 
        temp[i] = 0; 
    }

    /* Parte principale che svolge tutto il lavoro di somma. */

    int pariDispari;

    // Scopo del ciclo seguente è inizializzare i puntatori per i cicli interni.
    // Per farlo si usa l'indice pariDispari.
    // - pariDispari = 0 i cicli interni si inizializzano sui numeri pari.
    // - pariDispari = 1 i cicli interni si inizializzano sui numeri dispari.

    for (pariDispari = 0; pariDispari < 2; pariDispari++){

        // Trovo totale numeri in posizione pari/dispari 
        int totale = 0;
        for(k = pariDispari; k < n; k = k + 2){
            totale = totale + current[k]; // somma dei dispari
        }
        
        // Somma numeri successivi al corrente in posizione pari/dispari.
        // La somma avviene con il numero corrente e il totale dei suoi precedenti.

        int totalePrecedenti = 0;
        
        for( i = pariDispari; i < n; i = i + 2 ){
            
            // calcolo totale precedenti
            for( k = pariDispari; k < i ; k = k + 2 ){
                totalePrecedenti = totalePrecedenti + current[k];  
            }
            
            // calcolo somma dei numeri successivi al corrente
            temp[i] = totale - totalePrecedenti; 
            
            // azzero per nuova somma per futura iterazione
            totalePrecedenti = 0; 
        }
    }

   /* passo i dati dall'array temporaneo all'array del puntatore */
    for( i = 0; i < n; i++ ) {
        current[i] = temp[i];
    }    
    
}
```
