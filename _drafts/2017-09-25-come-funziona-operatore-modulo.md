---
title: Come funziona l'operatore modulo
summary: Metodo grafico per capire come funziona l'operatore modulo.
featured:
  show: yes
  image: ""
  image_from_url: "https://images.unsplash.com/photo-1535378620166-273708d44e4c?ixlib=rb-1.2.1&auto=format&fit=crop&w=2666&q=80"

categories: [linguaggio c, html]
---

```
// 3 modulo 10
// 10 modulo 10

0 1  2  3  4  5  6  7  8  9  0  1  2  3  4  5  6  7  8  9  0  
|----------------------------|-----------------------------|
0 1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18 19 20
        ↓                    ↓
        ↓                    10 mod 10 = 0 
        3 mod 10 = 3
```

```
//12 % 10

0 1  2  3  4  5  6  7  8  9  0  1  2  3  4  5  6  7  8  9  0  
|----------------------------|-----------------------------|
0 1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18 19 20
                                   ↓ 
                                   12 mod 10 = 2
```

```
//12 % 8

0 1  2  3  4  5  6  7  0  1  2  3  4  5  6  7  0  
|----------------------|-----------------------|
0 1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16
                                   ↓ 
                                   12 mod 8 = 4
```