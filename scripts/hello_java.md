### Java

```shell script
$ javac HelloJava.java
$ strace -c -U time-total,calls,errors java HelloJava
Hello from Java!
    seconds     calls    errors syscall
----------- --------- --------- ----------------
   0.012145       159        41 total
```