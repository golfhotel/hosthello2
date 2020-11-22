---
title: Lista di elementi concatenati semplici
layout: post
date: 2020-01-03
author: Ivan Garrini
categories: [linguaggio c]
summary: Le liste di elementi spiegate nell'ambito della programmazione.  
featured:
  show: true
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1576843018966-8c9e0d9d64cd?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70"
  image_alt: "Sono l'alt dell'immagine"
  image_title: "Sono il title dell'immagine"
sidebar: false 
latest_posts:   yes
---

La lista di elementi concatenate semplici sono un insieme di nodi dove ogni nodo è inteso come elemento della lista. 

## Lista della spesa su carta

Se prendiamo una tipica lista della spesa scritta a **penna** su un foglio di carta, potrebbe apparire come segue. Consideriamo la penna perchè i prodotti che scriviamo sulla carta vogliamo trattarli come non cancellabili dal foglio di carta stesso, ma piuttosto depennabili. 

---

**Lista spesa**

* acqua
* caffe
* sapone
* ecc...

---

Rapportando la lista sopra alla *lista di elementi concatenati* che andremo a trattare, ogni elemento della lista spesa (esempio il caffè) è un **nodo** della lista concatenata. 

Il termine concatenato fa riferimento al fatto che il prodotto *corrente* sulla carta è disposto in modo da avere un prodotto *predecente* al corrente e uno *successivo*: il prodotto precedente a **caffè** è **acqua** mentre il successivo è **sapone**. Ovviamente esiste il caso in cui il primo prodotto (acqua) non ha un precedente e che l'ultimo prodotto (sapone) non ha un successivo. 

Di seguito alcune azioni che possiamo compiere sulla lista scritta a penna su carta:

* per aggiungere un prodotto, prendiamo la penna e lo scriviamo inserendolo a fine lista. 

* per cancellare un prodotto lo depenniamo (tiriamo una riga sul prodotto) e lo sostituiamo scrivendo un nuovo prodotto al suo fianco. 

* oppure è possibile cancellare il prodotto (depennandolo) e basta.

* ecc...

Tenendo a mente queste "azioni" eseguibili sulla lista scritta su foglio di carta, andiamo a trattare la lista con elementi concatenati scritta in `C`.

## Lista concatenata in `C`. 

Si parte dal presupposto che la lista concatenata **deve** far uso delle **strutture**. Le strutture usate per creare la lista e i suoi elementi possono essere modellate in modi diversi. Questo aspetto sarà chiaro più avanti. 

```
//librerire usate da alcune funzioni
#include <stdlib.h>
#include <stdio.h>
#include <stdbool.h>

//dichiarazione struttura secondaria
struct node_t{
	int value;
	struct node_t *next;
};

//dichiarazione struttura principale
struct list_t{
	struct node_t *head; //deve essere già dichiarata la struct node_t
};
```

Si dichiara la struttura principale `struct list_t` formata da una variabile che dovrà contenere un indirizzo di memoria (quindi è una variabile puntatore). Possiamo vedere che la struttura principale è in seconda posizione rispetto alla struttura secondaria. Questo perchè `struct list_t` contiene il puntatore `*head` di tipo `struct node_t`. 

`struct node_t` che deve esser già dichiarato per essese usato da `struct list_t`. Diversamente si ha un errore di compilazione. 

```c
//firme funzioni
struct list_t *new_list();
void insert_on_head(struct list_t *list, int value);
void insert_on_tail(struct list_t *list, int value);
bool contains(struct list_t *list, int value);
void remove_from_list(struct list_t *list, int value);
void print(struct list_t *list);
void empty_list(struct list_t *list);
void free_list(struct list_t *list);
```

Guardando le firme delle funzioni possiamo vedere che ogni funzione riceve la lista per *indirizzo*.

```c
//funzione principale
void main(){
    
    //dichiaro un puntatore di tipo struct list_t
	struct list_t *list = new_list();

	int v;
	for(v = 0; v < 10; v++){
		insert_on_head(list, v);
	}
	print(list);
	for(v = 11; v < 20; v++){
		insert_on_tail(list, v);
	}
	print(list);

	if(contains(list, 5)){
		printf("list contains the value 5\n");
	}
	else{
		printf("list does not contain the value 5\n");
	}
	if(contains(list, 30)){
                printf("list contains the value 30\n");
        }
        else{
                printf("list does not contain the value 30\n");
        }

	remove_from_list(list, 5);
	print(list);
	if(contains(list, 5)){
                printf("list contains the value 5\n");
        }
        else{
                printf("list does not contain the value 5\n");
        }

	empty_list(list);
	print(list);
	insert_on_tail(list, 5);
	print(list);
	remove_from_list(list, 5);
	print(list);

	free_list(list);
};



struct list_t *new_list(){
	struct list_t *list = (struct list_t *)malloc(sizeof(struct list_t));
	list->head = NULL;
	return list;
};

void insert_on_head(struct list_t *list, int value){
	struct node_t *node = (struct node_t *)malloc(sizeof(struct node_t));
	node->value = value;
	node->next = list->head;
	list->head = node;
};

void insert_on_tail(struct list_t *list, int value){
	if(list->head == NULL){
		insert_on_head(list, value);
	}
	else{
		struct node_t *current = list->head;
		while(current->next != NULL){
			current = current->next;
		}
		struct node_t *node = (struct node_t *)malloc(sizeof(struct node_t));
	        node->value = value;
		node->next = NULL;
		current->next = node;
	}
};

bool contains(struct list_t *list, int value){
	struct node_t *current = list->head;
	while(current != NULL){
		if(current->value == value){
			return true;
		}
		current = current->next;
	}
	return false;
};	

void remove_from_list(struct list_t *list, int value){
	struct node_t *current = list->head;
	struct node_t *previous = NULL;
	while(current != NULL){
		if(current->value == value){
			if(current == list->head){
				list->head = current->next;
				free(current);
			}
			else{
				previous->next = current->next;
				free(current);
			}
			return;
		}
		previous = current;
		current = current->next;
	}
};

void print(struct list_t *list){
	if(list->head == NULL){
		printf("list is empty\n");
		return;
	}

	struct node_t *current = list->head;
	while(current != NULL){
		printf("%i ", current->value);
		current = current->next;
	}
	printf("\n");
};


void empty_list(struct list_t *list){
	struct node_t *current = list->head;
	struct node_t *previous = NULL;
	while(current != NULL){
		if(previous != NULL){
			free(previous);
		}
		previous = current;
		current = current->next;
	}
	if(previous != NULL){
		free(previous);
	}
	list->head = NULL;
};


void free_list(struct list_t *list){
	empty_list(list);
	free(list);
};

```


```c
//creazione lista 
//list è stato allocato con malloc())
//*head è puntato a NULL (= lista vuota, senza elementi)
   [0x55869911b010]  
    ↑     [NULL] 
    │     ↑
   list - *head

//nota: head deve contenere un indirizzo di una struct dello stesso tipo del puntatore *head. Quando c'è NULL non si ha nessun indirizzo per cui il puntatore *head non punta a niente
```

```c
//creazione elemento e inserimento in testa
// 
   [0x55869911b010] 
    ↑     [0x55869911b440]
    │     ↑
   list-*head ┬ .value 
               └ *next

   [0x55869911b440]
   ↑
   node ┬ .value = 100
   		 └ *next = NULL

```



event ┬ .sdate ┬ .day       10
      │        ├ .month     6
      │        └ .year      2016
      └ .stime ┬ .hour      15
               ├ .minute    33
               └ .second    59