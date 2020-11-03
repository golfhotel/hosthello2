---
layout: post
title:  Puntatori e array di caratteri
date:   2017-01-24
author: Ivan Garrini
categories: [linguaggio c]
summary: Note sulla distinzione tra puntatori a caratteri e array di caratteri.  
featured:
  show: false
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1602428142651-12dc685c73b0?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=630&q=70"
  image_alt: "Sono l'alt dell'immagine"
  image_title: "Sono il title dell'immagine"
sidebar: false 

---

Un *puntatore ad array* è comunemente usato nelle stringhe, ovvero negli array di caratteri: quando si parla di stringhe, si parla quindi di **puntatore ad array di caratteri**.

```c
//tipica stringa
char s[81] = "Stringa di caratteri";
```

Di norma in C, quando si usa una stringa **si genera un puntatore alla stringa** stessa (all'elemento con indice 0 dell'array), senza il bisogno di definirne il puntatore. Fare una cosa del tipo ```scanf(" %s", s);``` fa capire che non è necessario usare il simbolo ```&``` prima di s per identificare l'indirizzo dell'array (cosa che normalemente si fa quando si usa scanf per esempio con gli interi); questo perchè usare solo ```s``` è come usare ```&s[0]```, ovvero l'indirizzo del primo elemento dell'array.

```
     ┌ s equivale ad &s[0] 
     │
 [i] 0 1 2 3 4 5 6 7 8          ...        20
     │ │ │ │ │ │ │ │ │                     │                    
  s{ S,t,r,i,n,g,a, ,d,i, ,c,a,r,a,t,t,e,r,i }
```

Essendo ```s``` equivalente ad ```&s[0]```, si verifica che ```s``` è anche un puntore all'array ```s[]``` . 

Ora è bene distinguere un *comportamento* tra "puntatori a caratteri" ed "array di caratteri": 

```c
//assegnamento valido
char *text_ptr; //puntatore a caratteri
text_ptr = "Una stringa"; //assegno al puntatore un array di char

//assegnamento NON valido
char text[80]; //array di caratteri
text = "Non valido";
```

Un modo per **inizializzare** un array di caratteri è **inizializzare l'array al momento della sua dichiarazione**, come nel seguente modo:

```c
//dichiaro e inizializzo array di caratteri
char text[80] = "Valido";
```

Altro modo è inizializzare un array di caratteri via prompt:

```c
//inizializzo array tramite funzione scanf()
char text[81];
printf("Digita la stringa:\n");
scanf(" %s", text );
```

```c
//inizializzo array tramite funzione getchar()
char text[81];
printf("Digita la stringa:\n");
int i = 0;

do{
    s[i++] = getchar();
}while( s[i - 1] != '\n' );

s[i - 1] = '\0'; //tipicamente una stringa termina con valore nullo
```

**Ricorda.** L'istruzione `s[i++] = getchar();` prima assegna a `s` il valore restituito da `getchar()` e poi incrementa l'indice `i`.


