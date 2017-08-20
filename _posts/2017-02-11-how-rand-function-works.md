---
layout: post
title:  "Come si usa la funzione rand()"
date:   2017-02-11
categories: linguaggio c
summary: Capire la funzione rand() con spiegazione e semplici esempi.  
featured: yes
---

# Come si usa la funzione `rand()`

Per usare ```rand()``` bisogna inizializzare (basta una volta) il "generatore di numeri random".

```c
//inizializzazione generatore di numeri random
srand(time(NULL));
```

Quando si invoca la funzione ```rand()``` questa restituisce un valore casuale (o random) compreso in un certo intervallo. Se questo intervallo non è definito, si usa un intervallo di default che va da ```0``` a ```32766```, per cui ```rand()``` restituisce in modo casuale numeri interi che vanno da **0** a **32766**. Essendo incluso anche lo ```0```, il **totale** dei numeri gestiti da ```rand()``` è ```32767``` (che è diverso da 32766!!!). 

Questo numero totale è chiamato ```RAND_MAX``` interpretabile come la "dimensione" del range. 

Ora sapendo che ```RAND_MAX``` è il totale dei numeri gestibili con la funzione ```rand()```, possiamo dire che il più piccolo di questo totale di numeri è ```0``` mentre il più grande è ```RAND_MAX-1```

```
n.ro più piccolo      RAND_MAX-1
  ↑                       ↑
+---+---+---+---+-----+-------+
| 0 | 1 | 2 | 3 | ... | 32766 |
+---+---+---+---+-----+-------+
⌊______________________________⌋
               ↓
       RAND_MAX == 32767
```

**Per capire meglio.** Se non fosse stato considerato lo ```0``` e si partiva da ```1```, la dimensione totale (```RAND_MAX```) coincideva con il numero più grande del range (che non si sarebbe chiamato ```RAND_MAX-1``` ma ```RAND_MAX```) .

## Definire un intervallo per ```rand()```

Se ```RAND_MAX-1``` è il valore random più grande restituito da ```rand()```, il valore più piccolo è ```0```.

Quindi se non specificato diversamente, la funzione ```rand()``` restituisce un valore casuale da ```0``` a ```RAND_MAX-1```.

```c
//rand() restituisce in n valori casuali da 0 a 32766
n = rand();
```
Il codice sopra può essere scritto anche come il seguente.

```c
//RAND_MAX di default vale 32767
//rand() restituisce valori da 0 a RAND_MAX-1
//rand() restituisce in n valori casuali da 0 a 32766
n = rand() % 32767 ;
//rand() e rand() % 32767 sono identiche. 
```

È possibile definire un totale ```RAND_MAX``` diverso da quello di default usando il segno ```%```.

```c
//RAND_MAX == 100;
//rand() restituisce valori da 0 a RAND_MAX-1
//rand() restituisce in n valori casuali da 0 a 99
n = rand() % 100;
//  ⌊___________⌋
//        ├───────────── se (rand() % 100) restituisce 0  , n == 0
//        └───────────── se (rand() % 100) restituisce 100, n == RAND_MAX-1 == 99
```

Genericamente è possibile definire intervalli diversi in questo modo:

```c
n = ( rand() % max ) + min;
//  ⌊______________⌋
//         ├───────────── se (rand() % max) restituisce 0    , n == +min
//         └───────────── se (rand() % max) restituisce max-1, n == (max-1)+min
//Ricorda che rand() fornisce valori da 0 a RAND_MAX-1
``` 

Vediamo un esempio con i numeri.

```c
//Valori tra 5 e 100
n = ( rand() % 96 ) + 5;
//  ⌊_____________⌋
//         ├───────────── se (rand() % 95) restituisce 0 , n == +5
//         └───────────── se (rand() % 95) restituisce 95, n == 95+5 == 100
//Ricorda che rand() fornisce valori da 0 a RAND_MAX-1

//Valori tra -100 e 100
n = ( rand() % 201 ) - 100;
//  ⌊______________⌋
//         ├───────────── se (rand() % 201) restituisce 0  , n == -100
//         └───────────── se (rand() % 201) restituisce 200, n == 200-100 == 100
//Ricorda: rand() fornisce valori da 0 a RAND_MAX-1
```

## Definire un intervallo usando ```scanf()``` 

Se il range si riceve in input con (es.) ```scanf()```, bisogna calcolare ```RAND_MAX```. Per calcolarlo e sufficiente sottrarre dal ```max``` il ```min``` e aggiungere ```1```.

```c
//in generale
n = [ rand() % (max - min + 1) ] + min;
//             ⌊_____________⌋
//                    ↓
//                 RAND_MAX
```
Questo medoto vale sempre. Vediamo qualche esempio.

```c
//valori inseriti in input tramite scanf() 
//min == 5 e max == 100.
//tecnicamente RAND_MAX deve essere 96 ovvero 100-5+1 quindi max-min+1.

//Valori tra 5 e 100.
n = [ rand() % (100 - 5 + 1) ] + 5;
//  ⌊________________________⌋
//              ├───────────── se (rand() % (95 + 1)) restituisce 0 , a == +5
//              └───────────── se (rand() % (95 + 1)) restituisce 95, a == 95 + 5 == 101
//Ricorda che rand() restituisce valori da 0 a RAND_MAX-1
```

```c
//valori inseriti in input tramite scanf() 
//min == -100 e max == 100.
//tecnicamente RAND_MAX deve essere 201 ovvero 100-(-100)+1 quindi max-min+1.

//Valori tra -100 e 100.
n = [ rand() % (100 - (-100) + 1) ] + (-100);
//  ⌊_____________________________⌋
//              ├───────────── se (rand() % (100 - (-100) +1)) restituisce 0  , a == -100
//              └───────────── se (rand() % (100 - (-100) +1)) restituisce 200, a == 200 - 100 == 100
//RAND_MAX == (100 - (-100) +1) == 201
//Ricorda: rand() restituisce valori da 0 a RAND_MAX-1
```