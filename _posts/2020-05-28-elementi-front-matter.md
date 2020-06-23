---
title: Elementi del Front Matter nei posts per capire as.
summary: "Contiene tutti gli elementi del Front Matter. Quis non ea culpa magna labore elit sint est. Contiene tutti gli elementi del Front Matter. Contiene tutti as. "
author: Romolo
featured:
  show: true
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1568198473832-b6b0f46328c1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1592&q=80"
  image_alt: "Sono l'alt dell'immagine"
  image_title: "Sono il title dell'immagine"
categories: [front matter]
sidebar: 
  - trujillo: true
    related_posts: true

---

Nei post è possibile compilare alcuni campi presenti nella parte frontale del file ```.md``` o ```.html```. 

Questi campi sono chiamati *campi del Front Matter* e sono delle variabili con un valore. Per dichiararle e renderle usabili, queste variabili devono essere precedute e seguite da **tre trattini**. Vedi l'esempio seguente: 

```
---
variabile1: valore della variabile 1
variabile2: valore della variabile 2
---

Contenuto del post...
```

Nel Front Matter del post possiamo trovare le seguenti variabili.

## Title

Genera un titolo per il post.

```
---
title: Titolo del post
---
```

**Default:** se vuota o inesistente, il titolo del post sarà il nome del file. Ad esempio il file con il seguente nome ```2020-05-28-elementi-front-matter.md``` avrà il seguente titolo del post "**Elementi Front Matter**".

## Summary

Genera una descrizione del post ed è usata nell ```meta tag``` del codice ```html``` e in alcune miniature del post.

```
---
summary: Sono la descrizione del post.
---
```

## Author

Se presente, assegna il nome dell'autore al post.

```
---
author: Nome autore del post
---
```

**Default:** se il campo è vuoto o inesistente l'autore del post sarà quello specificato nella variabile ```author``` del file ```_config.yml``` accessbile tramite il tag {% raw %}```{{site.author}}```{% endraw %}.

## Featured

Identifica il post come un post **featured** e lo visualizza nel blog (o altre sezioni del tema) con uno stile CSS diverso.

**Per l'utilizzo** richiede specificare ulteriori campi.

```
featured:
  show: yes
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1465990138262-b7c355d1ef90?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2550&q=80"
```

```
code
```

Pariatur consequat ipsum cupidatat nostrud sint quis do mollit. Et qui eiusmod pariatur ad. Eiusmod deserunt enim labore consectetur excepteur in consectetur esse minim dolor commodo. Consequat veniam voluptate amet incididunt culpa magna et laboris quis ea nostrud enim elit id. Enim enim laborum culpa duis anim quis laboris quis.

Consequat consectetur deserunt nisi reprehenderit laborum labore consectetur. Adipisicing excepteur dolor nulla nulla commodo exercitation cupidatat fugiat dolore adipisicing. Adipisicing fugiat incididunt qui culpa ut et do fugiat sunt aliquip id cupidatat.

## Culpa aliqua velit eu veniam pariatur labore cillum cupidatat.

Fugiat qui incididunt nulla exercitation irure dolor excepteur excepteur sit. Est labore cillum ipsum ut mollit voluptate est culpa aute cupidatat sint sint reprehenderit nulla. Lorem mollit eiusmod dolore sunt quis cupidatat voluptate anim sunt anim dolor tempor nostrud deserunt. Mollit fugiat consequat anim commodo do.

Excepteur nulla tempor incididunt irure. Quis non nulla quis aliquip laborum cillum adipisicing est. Quis aute ea eiusmod commodo adipisicing velit proident non in. Nisi in exercitation ad eiusmod duis et voluptate anim. Commodo veniam nulla labore nisi. Consectetur est aute in pariatur dolor et velit ad sunt nisi veniam labore officia.

In dolore laboris occaecat in aliqua labore. Eiusmod aute et ad exercitation anim mollit sunt. Voluptate cillum laboris sunt do consectetur magna incididunt sunt incididunt magna in incididunt. Quis voluptate commodo minim Lorem ea sint ipsum do pariatur cillum. Magna dolor incididunt deserunt duis laborum officia Lorem sint ipsum labore excepteur incididunt consectetur. Commodo fugiat ad laboris cillum veniam.