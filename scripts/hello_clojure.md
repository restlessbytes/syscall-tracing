## Clojure

### 1. Run as script

```shell script
$ strace -c -U time-total,calls,errors clojure -M hello.clj 
Hello from Clojure!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.112218       520        83 total
```

### 2. Run through lein

```shell script
$ strace -c -U time-total,calls,errors lein run
Hello from Clojure!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.377057       780       114 total
```

### 3. Compile and run as uberjar (via lein)

```shell script
$ lein uberjar
Compiling hello-clj.core
Created /home/markus/programming/syscall_tracing/hello_clj/target/uberjar/hello_clj-0.1.0-SNAPSHOT.jar
Created /home/markus/programming/syscall_tracing/hello_clj/target/uberjar/hello_clj-0.1.0-SNAPSHOT-standalone.jar
$ strace -c -U time-total,calls,errors java -jar target/uberjar/hello_clj-0.1.0-SNAPSHOT-standalone.jar 
Hello from Clojure!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.044244       175        41 total
```
