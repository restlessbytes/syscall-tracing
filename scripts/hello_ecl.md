## Embedded Common Lisp (ECL)

**NOTE**: The source code is here is shared with SBCL

##### 1. Run as script
```shell script
$ strace -c -U time-total,calls,errors ecl --shell hello.lisp 
Hello from SBCL!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.001654       336        32 total
```

##### 2. Compile and run
```lisp
$ ecl 
> (compile-file "hello.lisp" :system-p t)
    ;;; Loading #P"/usr/lib/x86_64-linux-gnu/ecl-16.1.3/cmp.fas"
    ;;; Compiling hello.lisp.
    ;;; OPTIMIZE levels: Safety=2, Space=0, Speed=3, Debug=0
    ;;;
    ;;; Compiling (DEFUN GREET ...).
    ;;; End of Pass 1.
    ;;; Emitting code for GREET.
    ;;; Finished compiling hello.lisp.
    ;;;
    #P"/home/markus/programming/syscall_tracing/hello.o"
    NIL
    NIL
> (c:build-program "hello_ecl" :lisp-files '("hello.o"))
#P"hello_ecl"
> (compile-file "hello.lisp" :system-p t)
    ;;;
    ;;; Compiling hello.lisp.
    ;;; OPTIMIZE levels: Safety=2, Space=0, Speed=3, Debug=0
    ;;;
    ;;; Compiling (DEFUN GREET ...).
    ;;; End of Pass 1.
    ;;; Emitting code for GREET.
    ;;; Finished compiling hello.lisp.
    ;;;
#P".../hello.o"
> (c:build-program "hello_ecl" :lisp-files '("hello.o"))
#P"hello_ecl"
```

```shell script
$ strip ./hello_ecl
$ strace -c -U time-total,calls,errors ./hello_ecl
Hello from SBCL!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.000740       298        16 total
```
