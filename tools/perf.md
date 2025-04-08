# `perf`

https://jvns.ca/perf-zine.pdf

https://perfwiki.github.io/main/

https://documentation.suse.com/de-de/sles/12-SP5/html/SLES-all/cha-perf.html

#### List hardware events that perf can report with the current kernel and CPU

```sh
sudo perf list hw
```

#### Basic performance profiling (total CPU cycles used, instructions executed, cache misses, branch mispredictions)

```sh
sudo perf stat -e cycles,instructions,cache-misses,branch-misses ./<executable>
```

#### Function-level profiling

```sh
sudo perf record -g ./<executable>
sudo perf report
```

#### See real-time performance (for long-running programs)

```sh
sudo perf top
```

#### Analyze CPU-bound code at the assembly level

```sh
sudo perf annotate
```