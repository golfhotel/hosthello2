# Aritmetica dei puntatori

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