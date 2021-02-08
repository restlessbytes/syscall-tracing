## Racket

### 1. Run as script

```shell scriptell script
$ strace -c -U time-total,calls,errors racket hello.rkt 
"Hello from Racket!"
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.001598      2904        89 total
```

### 2. Compile and run

```shell script
$ raco exe -o hello_rkt hello.rkt 
$ strace -c -U time-total,calls,errors ./hello_rkt 
"Hello from Racket!"
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.003183      1612        11 total
```
