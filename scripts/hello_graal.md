## GraalVM

### C (using LLVM)
```shell script
$ $GRAAL_HOME/languages/llvm/native/bin/clang -o hello_lli hello.c
$ strace -c -U time-total,calls,errors lli hello_lli 
Hello from C!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.003083       411        12 total
$ strace -c -U time-total,calls,errors ./hello_lli 
Hello from C!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.000000        34         2 total
$ $GRAAL_HOME/languages/llvm/native/bin/clang -o hello_lli_st -static hello.c
$ strace -c -U time-total,calls,errors ./hello_lli_st 
Hello from C!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.000523        12         1 total
```

### Python

```shell script
$ strace -c -U time-total,calls,errors graalpython hello.py 
Please note: This Python implementation is in the very early stages, and can run little more than basic benchmarks at this point.
Hello from Python!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.001441      1703        43 total
```

### JavaScript

```shell script
$ strace -c -U time-total,calls,errors js hello.js 
Hello from JavaScript!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.000292       262         5 total
$ strace -c -U time-total,calls,errors node hello.js
Hello from JavaScript!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.001197       196       101 total
```

### Java

```shell script
$ gjavac HelloJava.java 
$ strace -c -U time-total,calls,errors gjava HelloJava 
Hello from Java!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.010598       158        40 total
$ native-image HelloJava 
[hellojava:316335]    classlist:   1,315.78 ms,  0.96 GB
     ...
[hellojava:316335]      [total]:  23,559.40 ms,  2.25 GB
$ strace -c -U time-total,calls,errors ./hellojava 
Hello from Java!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.000687       128         3 total
```

(_Note_: "gjavac" and "gjava" are GraalVM's javac and java respectively)

### Clojure

#### 1. Native Image from JAR
```shell script
$ native-image -jar hello_clj-0.1.0-SNAPSHOT-standalone.jar --verbose --no-fallback --initialize-at-build-time -H:+JNI 
Executing [ ...
$ mv hello_clj-0.1.0-SNAPSHOT-standalone* hello_clj_native
$ strace -c -U time-total,calls,errors ./hello_clj_native 
Hello from Clojure!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.005229       127         3 total
```

#### 2. Statically linked image from JAR 

```shell script
$ native-image -jar hello_clj-0.1.0-SNAPSHOT-standalone.jar --verbose --no-fallback --initialize-at-build-time -H:+JNI --static 
Executing [ ...
$ mv hello_clj-0.1.0-SNAPSHOT-standalone* hello_clj_native_static
$ strace -c -U time-total,calls,errors ./hello_clj_native_static 
Hello from Clojure!
    seconds     calls    errors syscall
----------- --------- --------- ------------------
   0.000248        63         2 total
```
