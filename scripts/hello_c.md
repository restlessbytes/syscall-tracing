## C
```shell script
$ gcc -O2 -o hello hello.c
$ gcc -O2 -o hello_st -static hello.c
$ du -h hello hello_st
20K	  hello
852K  hello_st
$ strace -c -U time-total,calls,errors ./hello
Hello from C!
seconds     calls    errors syscall
----------- --------- --------- ----------------
0.000000        34         2 total
$ strace -c -U time-total,calls,errors ./hello_st
Hello from C!
seconds     calls    errors syscall
----------- --------- --------- ----------------
0.000000        12         1 total
```