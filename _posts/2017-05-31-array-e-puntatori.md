# Array e puntatori

Di seguito un esempio sulla differenza d'uso su come gli array possono essere gestiti con l'uso di puntatori, a dimostrazione di come (array e puntatore) siano due elementi equivalenti tra loro. 

## Versione con array

```
#include <stdio.h>

//prototipi (o firme)
void riempiArray( int [] );
void stampaArray( int [] );

int main(){
    int array[5] ;
    riempiArray( array );
    stampaArray( array );
}

void riempiArray( int a[] ){
    int i; 
    for(i = 0; i < 5; i++){
        a[i] = i;
    }
}

void stampaArray( int a[] ){
    int i; 
    printf("array { ");
    for(i = 0; i < 5; i++){
        printf("%i ", a[i] ) ;
    }
    printf("}\n");
}
```

Il codice sopra è un tipico esempio di come un array viene gestito. Nel `main` vengono richiamate le funzioni: 

```
riempiArray( array );
stampaArray( array );
```

Il parametro passato alle due funzioni è il nome dell'array (in qeusto caso il nome è proprio `array`). Possiamo scrivere in modo del tutto equivalente al precedente, il seguente codice:

```
riempiArray( &array[0] );
stampaArray( &array[0] );
```

dove `&array[0]` sarebbe l'indirizzo di memoria (indirizzo fisico) del **primo** elemento del'array. Per cui passare `array` o `&array[0]` è la stessa cosa. **Infatti quando si passa il nome dell'array ad una funzione è come se venisse passato l'indirizzo del primo elemento dell'array**.

```
//il nome di un array corrisponde all'indirizzo 
//dell'elemento in posizione 0 dell'array stesso
array == &array[0]
```

Il **prototipo** delle funzioni seguenti  

```c
void riempiArray( int [] );
void stampaArray( int [] );
```

equivale al seguente prototipo: 

```c
void riempiArray( int * );
void stampaArray( int * );
```

Il parametro formale `( int * )` o il parametro formale `( int [] )` sono la stessa cosa. Entrambi i parametri richiedono  che il valore sia un **indirizzo di memoria**.

## Versione con aritmetica puntatori
 
A fronte di quanto già visto, di seguito è riportata una versione del codice precedente che fa uso dei puntatori.

```
#include <stdio.h>

//prototipi (o firma)
void riempiArray( int * );
void stampaArray( int ** );

int main(){
    //dichiaro array
    int array[5] ;
    int * arrayPtr = array;
    riempiArray( &array[0] ); //equivalente a riempiArray( array );
    stampaArray( &arrayPtr );
}

void riempiArray( int *a ){
/* Equivalente
void riempiArray( int a [] ){   
*/
    int i; 
    for(i = 0; i < 5; i++){
        a[i] = i;
    }
}

void stampaArray( int **a ){
    int i; 
    printf("array { ");
    for(i = 0; i < 5; i++){
        printf("%i ", *(*a + i) ) ;
    /*  equivalente
        printf("%i ", *(*a + i) ) ;  
    */
    }
    printf("}\n");
}
```

I prototipi delle funzioni sono i seguenti:

```
//prototipi (o firma)
void riempiArray( int * );
void stampaArray( int ** );
```

Sebbene le funzioni facciano la stessa cosa, ossia (come visto nell'esempio precedente) lavorare su un array di interi, le loro firme sono state modificate per scopi didattici. 

```
void riempiArray( int * );
```

Nella prima firma (come già detto in precedenza) è rischiesto che alla funzione venga passato un **indirizzo di una cella memoria** che al suo interno contenga un valore **intero**. L'asterisco identifica proprio che il parametro passato **deve essere trattato** come un indirizzo di memoria! Se guardiamo nel `main`, quando si richiama la funzione, viene passato l'indirizzo dell'array, ossia l'indirizzo del primo elemento dell'array `&array[0]`.

```
void stampaArray( int ** );
```

Nella seconda firma troviamo due asterischi. La firma richiede che alla funzione venga passato un **indirizzo di una cella memoria** che al suo interno contenga un altro **indirizzo di una cella memoria** che al suo interno contenga un valore intero. 

```
// la memoria e il doppio asterisco

            Memoria calcolatore    
           +-------------------+       
     ...   │         ...       │  ...            
           +-------------------+       
 array[1]  │         200       │ 0x001001001036 (== &array[1])
           +-------------------+      
    array  │         100       │ 0x001001001028 (== &array[0])
           +-------------------+  
 arrayPtr  │      &array[0]    │ 0x001001001024 (== &arrayPtr )
           +-------------------+

// equivale al seguente

            Memoria calcolatore    
           +-------------------+       
     ...   │         ...       │  ...            
           +-------------------+       
 array[1]  │         200       │ 0x001001001036 (== &array[1])
           +-------------------+      
    array  │         100       │ 0x001001001028 (== &array[0])
           +-------------------+  
 arrayPtr  │   0x001001001028  │ 0x001001001024 (== &arrayPtr )
           +-------------------+
```

Si chiama doppio puntatore o puntatore di puntatore ed è importante capirlo perchè usato (ad es.) nelle matrice allocate dinamicamente (matrici che in fase di esecuzione possono aumentare o diminuire l'uso della memoria in base alla necessità e  **senza** dover ricompilare il programma - es. per aumentare il numero elementi della matrice -). Ovviamente può esistere anche un triplo puntatore ecc...

```
    // main
    // dichiarazione puntatore
    int * arrayPtr = array; // oppure int * arrayPtr = &array[0];
    ...
    //richiamo funzione passandogli un'indirizzo 
    stampaArray( &arrayPtr );
```

Se guardiamo nel `main` vediamo che per passare un indirizzo contenente un altro indirizzo, bisogna dichiarare un puntatore perchè è **l'unico mezzo disponibile capace di contenere un indirizzo di memoria** senza alterarne il significato. 

Infatti usare il codice sotto porterebbe ad un errore di compilazione dato che si sta inserendo l'indirizzo del primo elemento dell'array (`array` equivale ad `&array[0]`) in una varibile che deve contenere solo valori interi. 

```c
//errato
int arrayPtr = array;

//si sta inserendo un valore alfanumerico 0x001001001028 
//in una variabile che richiede solo valori numerici
```

### Passare ad una funzione un indirizzo di memoria

Per capire meglio il concetto di passare un indirizzo di memoria ad una funzione guardiamo il codice sotto.

```
// firma
void riempiArray( int * );

...

// richiamo funzione nel main
riempiArray( 0x001001001028 );
```

Sapendo che la funzione richiede un indirizzo di memoria come parametro, nulla vieta di poter passare alla funzione un vero indirizzo di memoria. Ma il problema è che l'uomo non ha accesso facile agli indirizzi di memoria che sono di gestione del calcolatore. 

Il codice sopra non è errato, ma richiederebbe la conoscenza dell'indirizzo da passare alla funzione. Gestire tale cosa in questo modo è improponibile dato che bisognerebbe scrivere ogni volta "a mano" l'indirizzo di memoria (che tra l'altro cambia in modo continuo sul calcolatore) e ricompilare il programma. 

Per cui si usa il segno `&` davanti alla variabile, `array[0]` ecc... che permette di estrapolare l'indirizzo di memoria in modo automatico.