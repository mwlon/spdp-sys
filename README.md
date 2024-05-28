# SPDP Rust Bindings

See
[the Texas State page](https://userweb.cs.txstate.edu/~burtscher/research/SPDPcompressor/)
for information about this lossless codec for numerical data.
Note that I am not the original author; this just binds to the original (v1.1)
C source code.

## Usage and Safety

READ THIS IF YOU WANT TO USE THE BINDINGS!

Unstated by the original authors, but to avoid segfaults and memory corrupts
during batches, note:

* Input buffers get modified, as well as output buffers.
* During compression, the output buffer must be at least `2 * n + 9` bytes long,
  where `n` is the length of the input buffer.
* During decompression, the input(!) buffer must be at least as long as the
  output buffer.
  To actually use this, you'll want to store both compressed and uncompressed
  sizes somewhere else, then populate an input buffer of length
  `max(input_size, output_size)` and an output buffer of length `output_size`.

## Also Relevant

* [Pcodec](https://github.com/mwlon/pcodec/):
  another lossless codec for numerical data; contains a CLI with
  with benchmarks that compare vs. SPDP and others.
