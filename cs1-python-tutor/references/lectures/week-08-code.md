# Week 8 code files

The code files shown in the week 8 lectures.

### `add2.asm`
```
// Reads and adds 2 numbers
read
store 90
read
store 91
add 90
write
stop
```

### `add2.vic`
```
800
490
800
491
190
900
0
```

### `max2.asm`
```
// Reads two numbers and prints their maximum
  read
  store x
  read
  store y
  sub x
  gotop YISMAX
  load x
  write
  goto END
YISMAX:
  load y
  write
END:
  stop
```

### `max2.vic`
```
800
490
800
491
290
709
390
900
511
391
900
0
```

### `sum.asm`
```
// Sums up a sequence of numbers that ends with a zero.
  load zero 
  store sum
LOOP:
  read
  store x
  gotoz END
  load sum 
  add x   
  store sum
  goto LOOP
END:
  load sum
  write
  stop
```
