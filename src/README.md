# WTX

A collection of different transport implementations and related tools focused primarily on web technologies. The GitHub project is available at <https://github.com/c410-f3r/wtx>.

## Performance

Many things that generally improve performance are used in the project, to name a few:

1. **Manual vectorization**: When an algorithm is known for processing large amounts of data, several experiments are performed to analyze the best way to split loops in order to allow the compiler to take advantage of SIMD instructions in x86 processors.
2. **Memory alocation**: Whenever possible, all heap allocations are called only once at the start of an instance creation and additionally, stack memory usage is prioritized over heap memory.
3. **Fewer dependencies**: Besides being `no_std`, by default no third-party will be injected leaving additional dependencies up to the user through the selection of Cargo features, which decreases compilation times by a large margin. For example, you can see the mere 18 dependencies required by the PostgreSQL client using `cargo tree -e normal --features postgres`.

Since memory are usually held at the instance level instead of being created and dropped on the fly, it is worth noting that its usage can growth significantly depending on the use-case. If appropriated, try using a shared pool of resources or try limiting how much data can be exchanged between parties.

## Benchmarks

If you disagree with any of the mentioned charts, feel free to checkout [wtx-bench](https://github.com/c410-f3r/wtx/tree/main/wtx-bench) to point any misunderstandings or misconfigurations.

There are mainly 2 things that impact performance, the chosen runtime and the number of pre-allocated bytes. Specially for servers that have to create a new instance for each handshake, pre-allocating a high number of bytes for short-lived or low-transfer connections can have a negative impact.

It is also possible to use libraries that manage pools of resources to avoid having to reconstruct expensive elements all the time.
