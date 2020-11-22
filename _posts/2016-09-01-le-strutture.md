---
title: Le strutture 
layout: post
author:   Ivan
categories: [linguaggio c]
summary:    
featured:
  show: false
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1493476523860-a6de6ce1b0c3?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70"
  image_alt: "Sono l'alt dell'immagine"
  image_title: "Sono il title dell'immagine"
sidebar: false
---

1. [Definire una struttura](#definire-una-struttura)
2. [Dichiarare una variabile di tipo struttura](#dichiarare-una-variabile-di-tipo-struttura)
3. [Accedere ad un’elemento di una struttura](#accedere-ad-unelemento-di-una-struttura)
4. [Inizializzare una variabile di tipo struttura](#inizializzare-una-variabile-di-tipo-struttura)

Una struttura è un **tipo di dato** come lo è ```int```, ```float```, ```char``` ecc... Ora i tipi di dato ```int```, ```float```, ```char``` (ecc...) sono tipi di dato già *definiti* nel linguaggio C per cui non è necessario ri-definirli. Non è necessario quindi dire al calcolatore cosa deve contenere ```int``` piuttosto che ```float``` ecc... È sufficiente *dichiarare* la variabile, array, funzione o altro per far si che si riservi una locazione di memoria. 

Per le strutture invece è diverso. **È necessario** prima **definire una struttura** per dire al compilatore come vogliamo *personalizzare* questo tipo di dato. Definire una struttura non alloca memoria, quindi definire non vuol dire riservare. 

Successivamente alla definizione bisogna "inizializzare" la variabile di tipo struttura. Inizializzare ha sottinteso il senso di dover riservare della memoria e quindi si avrà fisicamente un "luogo" nel calcolatore riservato alla variabile, array o altro.

## Definire una struttura
Di seguito ***definiamo una struttura*** chiamata ```date```. Possiamo vedere che è composta da tre elementi: ```int day;```, ```int month;``` e ```int year;```. 

```c
struct date{
    int day;
    int month;
    int year;
};  // importante ricordare il punto e virgola!
```
Cosi facendo abbiamo creato un nuovo ***tipo di dato***  chiamato appunto ```struct date```. 

## Dichiarare una variabile di tipo struttura

Per capire meglio ricordiamo che con 

```c
int contatore;
```
dichiariamo una varibile di tipo ```int``` di nome ```contatore```. 

Invece con la seguente dichiarazione 

```c
struct date today;
```   

dichiariamo una variabile di tipo ```struct date``` di nome ```today```.

Da notare subito che nella struttura abbiamo prima **definito il tipo di dato struttura** e poi **dichiarato la variabile di tipo struttura**. Mentre nel tipo di dato ```int``` non abbiamo *definito* niente perchè ```int``` è un tipo di dato gia "definito" di default nel linguaggio ```c```, quindi già esiste a priori!

## Accedere ad un'elemento di una struttura

Possiamo accedere ed impostare un valore ad un'elemento di una struttura nel seguente modo

```c
today.day = 25;
today.month = 5;
today.year = 2016;
```

## Inizializzare una variabile di tipo struttura

Possiamo inizializzare una struttura nel seguente modo:

```c
//inizializzo tutti gli elementi
struct date today = { 25, 5, 2016 }; 
//inizializzo parte degli elementi
struct date today = { 25, 5};        
```

Nota che con la modalità di sopra **devo rispettare l'ordine** con cui dichiaro gli elementi.

Altri modi di inizializzare una variabile di tipo struttura:

```c
//inizializzo tutti gli elementi
struct date today = { .day = 25,  .month = 5, .year = 2016 }; 
struct date today = { .month = 5, .day = 25,  .year = 2016 }; 
```

```c
//inizializzo tutti gli elementi (indentazione diversa)
struct date today = { 
    .day = 25, 
    .month = 5, 
    .year = 2016 
}; 
```

```c
//inizializzo parte degli elementi
struct date today = { .day = 25,  .month = 5 }; 
struct date today = { .month = 5, .day = 25  };
```

```c
// dichiaro la variabile today di tipo "struct date" 
struct date today;    

// inizializzo i valori 
today.day    = 25;    
today.month  = 1;     
today.year   = 2011;  
```

Nota che con le modailtà sopra **posso non rispettare l'ordine** con cui dichiaro gli elementi.

## Varibili standard e variabili strutture

Abbiamo detto che definire una struttura vuol dire definire un nuovo tipo di dato. Questo nuovo tipo di dato possiamo "customizzarlo" con elementi di nostro piacimento e non necessariamente uguali.  Infatti potremmo definire una struttura con elementi NON dello stesso tipo

```c
//definizione struttura
struct date{
    int day;
    int month;
    int year;
    char nota; //char è diverso da int
};

//dichiarazione variabile di tipo struct date
struct date today = { .day = 25, .month = 5, .year = 2016 };
```

Nota che una struttura è diversa da un'array (un array accetta elementi dello stesso tipo)!

![alt text](https://images.unsplash.com/photo-1555883006-37d106604feb?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70 "Logo Title Text 1")

Di una variabile di tipo struttura posso usare un elemento della struttura come una comune variabile comune e fare qualcosa come 

```c
century = today.year / 100 + 1;
```

## Funzioni e strutture

Normalmente nelle funzioni posso passare come parametro formale una variabile o un'array. Posso fare la stessa cosa con le struttura **possando una struttura come parametro formale** di una funzione.

```c
int numberOfDays (struct date d){ //il parametro formale è una struttura 
                                  
    /* codice funzione */
    
    return 0;
}
```
Il parametro formale è una variabile di tipo ```struct date```, quindi una struttura. È come dire che il parametro formale è una variabile di tipo ```int```, quindi un intero.

Con la funzione posso anche ritornare una variabile di tipo ```struct date```, quindi posso ritornare una struttura. 

```c
struct date changeDate(struct date d) {
    struct date result;
    
    result.day = d.day + 1;
    result.month = d.month + 1;
    result.year = d.year + 2;
    
    return result;
}
```

Nota che se all'interno della funzione la varibile di tipo ```struct date``` verrà modificata, la modifica avrà effetto solo all'interno della funzione. 
La variabile struttura non è un array per cui non ci saranno variabili di tipo ```struct date``` esterne alla funzione che subiranno modifiche.

## Array di strutture

Con la seguente istruzione dichiaro un semplice **array di interi**:

```c
int array[10];
```

Invece con la seguente istruzione dichiaro un **array di strutture**:

```c
struct date week[7];
```

Per inizializzare un array di strutture posso farlo cosi

```c
struct date week[7] = {
    {10, 6, 2016},   
    {11, 6, 2016},
    {12, 6, 2016}
};
```
Quella sopra puo essere considerata **definizione+inizializzazione** di un array di strutture. Si nota subito che sono stati *inizializzati* solo i primi tre elementi dell'array.

Visivamente l'array di strutture di sopra può essere interpretato così:

    week[0] ┬ .day      10
            ├ .month    6
            └ .year     2016
    week[1] ┬ .day      11
            ├ .month    6
            └ .year     2016
    week[2] ┬ .day      12
            ├ .month    6
            └ .year     2016
            
## Strutture contenenti strutture

```c
// definisco una struttura contenente strutture
struct dateAndTime{
    struct date sdate;
    struct time stime;
};
```

Nota che l'uso della struttura ```struct dateAndTime``` richiede che le seguenti strutture siano state definite in precedenza! 

```c
    struct date sdate;
    struct time stime;
``` 

Definita la struttura, possiamo dichiarare una variabile di tipo ```struct dateAndTime```:

```c
// dichiaro la variabile event di tipo "struct dateAndTime"
struct dateAndTime event;
```

Visivamente possiamo vederla così:

    event ┬ .sdate ┬ .day       10
          │        ├ .month     6
          │        └ .year      2016
          └ .stime ┬ .hour      15
                   ├ .minute    33
                   └ .second    59
                   
Ecco la sintassi per far riferimento ad una struttura della variabile ```event```.

```c
// riferimento alla struttura date della varibile event
event.sdate
```

```c
// riferimento al membro "month" della struttura date della varibile event
event.sdate.month = 10;

// incremento il membro month
++event.sdate.month;
```

Per inizializzare la varibile ```event```

```c
struct dateAndTime event = {
  { 3, 9, 2016 },
  { 4, 9, 2016 }
};

// usando i nomi membri 
struct dateAndTime event = {
  { .day = 3,   .month = 9, .year = 2016 },
  { .month = 9, .day = 4,   .year = 2016 }
};
```

Nel codice precedente abbiamo usato dichiarato la *variabile* ```event``` di tipo ```struct dateAndTime```. 

Nulla vieta di dichaiarare anche un **array** di nome ```events``` di tipo ```struct dateAndTime```:

```c
// dichiaro array di 3 elementi di tipo struct dateAndTime
struct dateAndTime events[3];
```

Visivamente possiamo vederlo cosi: 

    events[0] ┬ .sdate ┬ .day       
              │        ├ .month     
              │        └ .year      
              └ .stime ┬ .hour      
                       ├ .minute    
                       └ .second    
                      
    events[1] ┬ .sdate ┬ .day       
              │        ├ .month     
              │        └ .year      
              └ .stime ┬ .hour      
                       ├ .minute    
                       └ .second                      
                      
    events[2] ┬ .sdate ┬ .day       
              │        ├ .month     
              │        └ .year      
              └ .stime ┬ .hour      
                       ├ .minute    
                       └ .second    

Con il seguente codice, impostiamo la data e l'ora del primo elemento dell'array:

```c
// imposto data 
events[0].sdate.day   = 3;
events[0].sdate.month = 9;
events[0].sdate.year  = 2016;

// imposto ora 
events[0].stime.hour   = 3;
events[0].stime.minute = 9;
events[0].stime.second = 2016;
```

## Struttura contenenti array

Di seguito definiamo una struttura che contiene anche array. 

```c
struct month{
    int numberOfDays; // n.ro giorni del mese
    char name[3];     // nome abbreviato del mese
};
```

Sopra abbiamo definito una struttura contenente un intero e un array di caratteri (tipicamente usato come stringa). 

Definiamo una varibile di tipo ```struct month```:

```c
struct month aMonth;
```

Inizializziamo la variabile ```aMonth```:

```c
struct month aMonth = {
    31;
    {'A', 'u', 'g'};
};
```

Oppure

```c
aMonth.numberOfDays = 31;
aMonth.name[0] = 'A';
aMonth.name[1] = 'u';
aMonth.name[2] = 'g';
```

Visivamente possiamo vederlo così:

    aMonth ┬ .numberOfDays  31
           └┬ .name[0]     'A'
            ├ .name[1]     'u'
            └ .name[2]     'g'         

## Array di strutture contenenti array

Di seguito definiamo una struttura che contiene anche array. 

```c
struct month{
    int numberOfDays; // n.ro giorni del mese
    char name[3];     // nome abbreviato del mese
};
```

Dichiaro l'**array** ```months``` di tipo ```struct month```:

```c
struct month months[12];
```

Inizializziamo l'array ```months```:

```c
// inizializzo parte dell'array
struct month months[12] = {
    { 31, {'G', 'e', 'n'} },    //months[0]
    { 28, {'F', 'e', 'b'} },    //months[1]
    { 31, {'M', 'a', 'r'} },    //months[2]
};
```

Oppure

```c
months[0].numberOfDays = 31;
months[0].name[0] = 'G';
months[0].name[1] = 'e';
months[0].name[2] = 'n';

months[1].numberOfDays = 28;
months[1].name[0] = 'G';
months[1].name[1] = 'e';
months[1].name[2] = 'n';

months[2].numberOfDays = 31;
months[2].name[0] = 'G';
months[2].name[1] = 'e';
months[2].name[2] = 'n';
```

Visivamente possiamo vederlo così:

    months[0] ┬ .numberOfDays  31
              └┬ .name[0]     'G'
               ├ .name[1]     'e'
               └ .name[2]     'n'
              
    months[1] ┬ .numberOfDays  28
              └┬ .name[0]     'F'
               ├ .name[1]     'e'
               └ .name[2]     'b'              

    months[2] ┬ .numberOfDays  30
              └┬ .name[0]     'M'
               ├ .name[1]     'a'
               └ .name[2]     'r'              

## Esempio complesso sull'uso delle strutture

Di seguito un esempio di come si potrebbero usare le strutture appena viste. Potremmo dire di usare una **array di strutture contenenti strutture contenti array**

Definisco la struttura ```date```:

```c
struct date{
    int day;
    int month;
    int year;
};
```

Definisco la struttura ```time```

```c
struct time{
    int hour;
    int minute;
};
```

Definisco la struttura ```detail```

```c
struct detail{
    char name[81];
    char surname[81];
    int telephone;
};
```

Definisco la struttura ```agenda```:

```c
struct agenda{
    struct date sdate;
    struct time stime;
    struct detail sdetail; // variabile di tipo struttura contiene un array
};
```

Dichiaro l'array  ```sappointment``` di tipo ```struct agenda```

```c
// dichiaro un array di 3 elementi di tipo "struct agenda"
struct agenda appointment[3];
```

Inizializzo l'array: 

```c
struct agenda appointment[3] = {
    {   // appointment[0]
        { 3, 9, 2016 }, 
        { 17, 5  }, 
        { {'M', 'a', 'r', 'i', 'o'}, {'R', 'o', 's', 's', 'i'}, { 123456789 } }
    }, 
    {   // appointment[1] 
        { 3, 9, 2016 }, 
        { 18, 10 }, 
        { {'T', 'i', 'z', 'i', 'o'}, {'B', 'i', 'a', 'n', 'i'}, { 987654321 } }
    },
    {   // appointment[2]
        { 4, 9, 2016 }, 
        { 15, 5  }, 
        { {'L', 'u', 'i', 'g', 'i'}, {'G', 'r', 'i', 't', 'i'}, { 5432198760 } }
    }
};
```

Per accede ai vari campi delle relative variabili/array possiamo farlo con l'uso di opportuni cicli ```for```, qui ommessi.

```c
// accedo ai campi della variabile sdate
appointment[0].sdate.day = 3;
appointment[0].sdate.month = 9;
appointment[0].sdate.year = 2016;

// accedo ai campi della variabile stime
appointment[0].stime.hour = 17;
appointment[0].stime.minute = 57;

// accedo all'array name della variabile sdetail
appointment[0].sdetail.name[0] = 'M';
appointment[0].sdetail.name[1] = 'a';
appointment[0].sdetail.name[2] = 'r';
appointment[0].sdetail.name[3] = 'i';
appointment[0].sdetail.name[4] = 'o';

// accedo all'array surname della variabile sdetail
appointment[0].sdetail.surname[0] = 'R';
appointment[0].sdetail.surname[1] = 'o';
appointment[0].sdetail.surname[2] = 's';
appointment[0].sdetail.surname[3] = 's';
appointment[0].sdetail.surname[4] = 'i';

// acccedo al campo della variabile sdetail
appointment[0].sdetail.telephone = 123456789;

// ecc...
```

Visivamente possiamo vederlo così:

    appointment[0] ┬ .sdate ┬ .day       
                   │        ├ .month     
                   │        └ .year
                   │
                   ├ .stime ┬ .hour       
                   │        └ .minute
                   │
                   └ .sdetail ┬─┬ .name[0]     
                              │ ├ .name[1]     
                              │ ├ ...
                              │ └ .name[i]
                              │
                              ├─┬ .surname[0]     
                              │ ├ .surname[1]     
                              │ ├ ...
                              │ └ .surname[i]                              
                              │
                              └ .telephone    

    ...

    appointment[2] ┬ .sdate ┬ .day       
                   │        ├ .month     
                   │        └ .year
                   │
                   ├ .stime ┬ .hour       
                   │        └ .minute
                   │
                   └ .sdetail ┬─┬ .name[0]     
                              │ ├ .name[1]     
                              │ ├ ...
                              │ └ .name[i]
                              │
                              ├─┬ .surname[0]     
                              │ ├ .surname[1]     
                              │ ├ ...
                              │ └ .surname[i]                              
                              │
                              └ .telephone                                
 


## Bibliografia o altri riferimenti
* [Programmare in C - Introduzione al linguaggio (Kochan - Pearson)](https://www.amazon.it/Programmare-C-Introduzione-al-linguaggio/dp/8871926609){:target="_blank"}