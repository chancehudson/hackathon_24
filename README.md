# PSE hackathon 2024 plan

Build a web ide/benchmarking utility for [ashlang](https://github.com/chancehudson/ashlang). [More info](https://github.com/chancehudson/ashlang/tree/main/src/r1cs#readme).

I'd like to build all of these things with equal priority. I'd like to build the features before the stretch features.

## IDE features

- [ ] static webpage with a text entry field
  - [ ] compile single function
- [ ] local function directory storage
  - [ ] use indexeddb or similar
  - [ ] export directory tarball
- [ ] getting started scripts
- [ ] links (repo, information, docs)
- [ ] compile code as it's written
  - [ ] show a green or red light if compilation succeeds or fails
  - [ ] show messages from the assembler
    - assembler will provide a standard message format
- [ ] builtin access to the [stdlib](https://github.com/chancehudson/ashlang/tree/main/stdlib)
- [ ] builtin access to the benchmark library (see below)
- [ ] basic syntax highlighting
- [ ] syntax completion for function names when a button is pressed
  - e.g.
    - i'm writing code and am about to invoke a function
    - `let x = `
  - [ ] i press `shift+space` and a list of _function names_ appears
  - [ ] the function _source code_ appears in a window next to the list
  - [ ] the function source changes with the _up/down arrow keys_
  - [ ] as i type the list is filtered and the **source code preview** changes
    - this is simple and fast, each include is a directory tree of function names
    - function name = filename without extension = `'pow5.ash'.split('.')[0]`
    - the file extension determines what functions can be called
    - `ash` -> calls everything, `tasm` -> calls nothing, `ar1cs` -> calls nothing
- [ ] r1cs binary file format
  - include [witness instructions](https://github.com/chancehudson/ashlang/tree/main/src/r1cs#symbolic-constraints) in the r1cs file
- [ ] green checkmark if the prover being targeted is post quantum secure

### Stretch features

- [ ] publish and share circuits (leetcode style)
- [ ] ai based auto-completion/suggestion (disabled for functions)

## Benchmark features

- [ ] numerous scripts designed to test different aspects of the language and prover
  - [ ] matrix multiplication, division, addition and subtraction
  - [ ] various permutations using these operations, e.g. prove `a[0..1024][0..1024] * b[0..1024][0..1024]`, `pow5(a[0..1024])`, `pow5_inv_sum(a[0..1024])`
  - [ ] stack depth tests
    - automatically generate a tree of functions to grow the stack
  - [ ] execute logic at different stack depths over time
    - pass arguments of various size to functions at various depths
- [ ] support for the following provers
  - [ ] [TritonVM](https://github.com/TritonVM/triton-vm)
  - [ ] [Spartan](https://github.com/microsoft/Spartan)
  - [ ] [Spartan2](https://github.com/microsoft/Spartan2)
  - [ ] [snarkjs](https://npm.com/snarkjs)
  - [ ] [arkworks](./.gitignore)
  - **your prover here**
- [ ] show information about proving time and circuit size
  - [ ] `tasm` targets
    - [ ] show [vm stats](https://github.com/TritonVM/triton-vm/issues/319#issuecomment-2290842186)
    - [ ] show proof _byte length_
  - [ ] `r1cs` targets
    - [ ] show number of signals
    - [ ] show number of constraints
    - [ ] show average number of signals per constraint (efficiency)
- [ ] include ability to "run all files in directory" and benchmark each one
  - e.g. for ci or device tests
- [ ] export benchmark to file (json is fine)

### Stretch features

- [ ] show graph visualization of `r1cs` constraint system
- [ ] analyze `r1cs` signal relationships
  - [ ] analyze the signal structure and visualize it in a graph?
    - [ ] goal is to provide data for implementing an optimizer
- [ ] public lists of benchmarks (e.g. recent benchmarks)
  - [ ] publish benchmark after running
    - [ ] optionally include hash of program that was run
    - [ ] optionally include anonymized device information

## Collaboration tools

- [ ] run a git server that _anyone_ can push to
  - [ ] mirror that server to a github pull request

## Chore tasks

- [ ] move [scalar field](https://github.com/chancehudson/ashlang/tree/main/src/math) implementations to a separate crate
  - [ ] curated implementions of each curve _scalar field_ into a single minimal _trait_

## Interested?

Preferred strategies:

- [dynamic web](https://github.com/Unirep/trusted-setup/tree/main/packages/frontend/src)
- [static web](https://github.com/chancehudson/keccak-doomsday/tree/main/web/src)
- [if you're a goat](https://github.com/emilk/egui)

## Repos i like right now

- [triton tui](https://github.com/TritonVM/triton-tui#readme)
  - simple and effective stack debugging
- [twenty-first](https://github.com/neptune-crypto/twenty-first#readme)
  - fast `2^64 - 2^32 + 1` (0xfoi) scalar field implementation
  - very nice api
