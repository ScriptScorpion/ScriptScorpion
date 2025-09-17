bitwise operations in C/C++ means that it goes for every bit in one number and second number and does mathematical operations with this bits.

`&` in C/C++ - it is just bitwise multiplication example in C/C++:  0b11 & 0b10 = 0b10

TABLE FOR `&`(**AND**):
```
0 | 0 = 0
0 | 1 = 0
1 | 0 = 0
1 | 1 = 1
```

`|` in C/C++ - it is just bitwise addition example in C/C++: 0b11 | 0b10 = 0b11

TABLE FOR `|`(**OR**):
```
0 | 0 = 0
0 | 1 = 1
1 | 0 = 1
1 | 1 = 1
```

`^` in C/C++ - it is just bitwise subtraction(expect negative values cannot be) example in C/C++: 0b11 ^ 0b10 = 0b1

TABLE FOR `^`(**XOR**):
```
0 | 0 = 0
0 | 1 = 1
1 | 0 = 1
1 | 1 = 0
```

examples of bitwise operations:

`Number & 1` - if Number is odd(devided by 2 and remainder is more then 0), then prints 1, else prints 0

`Number & 0` - prints 0, same as: Number ^ Number

`Number | 1` - if Number is even(devided by 2 and remainder is 0), then Prints (Number + 1), else prints just Number

`Number | 0` - Prints Number

`Number ^ 1` - Prints (Number - 1)

`Number ^ 0` - Prints Number
