## Build Executables / Images

**NOTE**: Source code is shared with ECL.

### 1. SBCL - Build Lisp Image

```shell script
$ sbcl
This is SBCL 2.0.1.debian, an implementation of ANSI Common Lisp.
More information about SBCL is available at <http://www.sbcl.org/>.

SBCL is free software, provided as is, with absolutely no warranty.
It is mostly in the public domain; some portions are provided under
BSD-style licenses.  See the CREDITS and COPYING files in the
distribution for more information.
* (defun greet () (write-line "Hello from SBCL!"))
GREET
* (sb-ext:save-lisp-and-die "hello_sbcl" :toplevel #'greet :executable t)
[undoing binding stack and other enclosing state... done]
[performing final GC... done]
[defragmenting immobile space... (fin,inst,fdefn,code,sym)=1030+939+18540+18889+26168... done]
[saving current Lisp image into hello_sbcl:
writing 0 bytes from the read-only space at 0x50000000
writing 384 bytes from the static space at 0x50100000
writing 29949952 bytes from the dynamic space at 0x1000000000
writing 2048000 bytes from the immobile space at 0x50300000
writing 12300288 bytes from the immobile space at 0x52100000
done]
```

### 2. SBCL - Executable using buildapp

```shell script
$ buildapp --eval '(defun main (argv) (write-line "Hello from SBCL!"))' \
   --entry main \
   --output hello_lisp
; in: DEFUN MAIN
;     (SB-INT:NAMED-LAMBDA MAIN
;         (ARGV)
;       (BLOCK MAIN (WRITE-LINE "Hello from SBCL!")))
; 
; caught STYLE-WARNING:
;   The variable ARGV is defined but never used.
; 
; compilation unit finished
;   caught 1 STYLE-WARNING condition
```

## Run Programs

### 1. Run as script

```shell script
$ strace -c -U time-total,calls,errors sbcl --script hello.lisp 
Hello from SBCL!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.000806       334        16 total
```

### 2. Compile and run as Lisp image

```shell script
$ strace -c -U time-total,calls,errors ./hello_sbcl 
Hello from SBCL!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.000860       233         4 total
```

### 3. Compile and run as binary using buildapp

```shell script
$ buildapp --eval '(defun main (argv) (write-line "Hello from SBCL!"))' \
   --entry main \
   --output hello_lisp
; in: DEFUN MAIN
;     (SB-INT:NAMED-LAMBDA MAIN
;         (ARGV)
;       (BLOCK MAIN (WRITE-LINE "Hello from SBCL!")))
; 
; caught STYLE-WARNING:
;   The variable ARGV is defined but never used.
; 
; compilation unit finished
;   caught 1 STYLE-WARNING condition
$ strace -c -U time-total,calls,errors ./hello_lisp 
Hello from SBCL!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.000497       225         4 total
```
