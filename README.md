# Syscall Tracing

This repository contains all source code, setup, build and run scrips (and commands) used in 
[this](http://www.restless-bytes.com/posts/of-the-tracing-of-syscalls) post.

It was inspired by another post which you can find [here](https://drewdevault.com/2020/01/04/Slow.html).

### Where's what?

1. Source files are located in `src/`.
2. `scripts/` contains scripts (who would've thought) and commands (in the form of shell output) for setup / build / 
run tasks.

### Platforms, Languages, Tools and Versions

- OS: Ubuntu 20.04.1 LTS (focal)
- Kernel: 5.4.0-58-generic GNU/Linux
- Hardware: 
  * System: Dell Notebook XPS 13 7390 (0962) 64 bits
  * Processor: Intel(R) Core(TM) i7-10510U CPU @ 1.80GHz
  * RAM: 2x 8GB DDR3
- strace: 5.10
- GCC: 9.3.0
- SBCL: 2.0.1.debian
- ECL: 16.1.3
- buildapp: 1.5.6
- Racket (+raco): v7.7
- Java: OpenJDK 13 (build 13.0.2+8)
- Clojure: 1.10.1
- Leiningen: 2.9.2
- GraalVM: CE 20.2.0 (using OpenJDK 11.0.8 2020-07-14)