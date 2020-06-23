---
title: Aritmetica dei puntatori
date: 2017-09-02 12:10:05
summary: Foo Bar Baz
categories: [html]

permalink: 

---

Lorem ipsum dolor sit, amet consectetur adipisicing elit. Harum deserunt sed itaque molestiae libero quibusdam, doloremque animi corporis laborum unde nihil molestias possimus ea. Provident nihil modi aspernatur hic consequatur?

Lorem ipsum dolor sit, amet consectetur adipisicing elit. Harum deserunt sed itaque molestiae libero quibusdam, doloremque animi corporis laborum unde nihil molestias possimus ea. Provident nihil modi aspernatur hic consequatur?




```
ptr++;    // Pointer moves to the next int position (as if it was an array)
++ptr;    // Pointer moves to the next int position (as if it was an array)
++*ptr;   // The value of ptr is incremented

++(*ptr); // The value of ptr is incremented
++*(ptr); // The value of ptr is incremented
*ptr++;   // Pointer moves to the next int position (as if it was an array). But returns the old content
(*ptr)++; // The value of ptr is incremented
*(ptr)++; // Pointer moves to the next int position (as if it was an array). But returns the old content
*++ptr;   // Pointer moves to the next int position, and then get's accessed, with your code, segfault
*(++ptr); // Pointer moves to the next int position, and then get's accessed, with your code, segfault

```

Lorem ipsum dolor sit, amet consectetur adipisicing elit. Harum deserunt sed itaque molestiae libero quibusdam, doloremque animi corporis laborum unde nihil molestias possimus ea. Provident nihil modi aspernatur hic consequatur?
