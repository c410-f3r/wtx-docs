# WTX

A collection of different transport implementations and related tools focused primarily on web technologies. The GitHub project is available at <https://github.com/c410-f3r/wtx>.

## Benchmarks

If you disagree with any of the mentioned charts, feel free to checkout [wtx-bench](https://github.com/c410-f3r/wtx/tree/main/wtx-bench) to point any misunderstandings or misconfigurations.

There are mainly 2 things that impact performance, the chosen runtime and the number of pre-allocated bytes. Specially for servers that have to create a new instance for each handshake, pre-allocating a high number of bytes for short-lived or low-transfer connections can have a negative impact.

It is also possible to use libraries that manage pools of resources to avoid having to reconstruct expensive elements all the time.
