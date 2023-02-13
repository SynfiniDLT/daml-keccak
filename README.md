# daml-keccak

Daml library containing an implementation of the Keccak hash function.

## Build

Run the following to compile the library as a DAR file:

```bash
cd main
daml build
```

## Importing the library

To import the library it is recommended to use a
[data-dependency](https://docs.daml.com/daml/intro/9_Dependencies.html#dependencies-and-data-dependencies). First, build
the library as described above, then add a dependency on the DAR file: `main/.daml/dist/keccak-<version>.dar`.

Please note: while it is possible to import internal modules using data dependencies, this is not recommended. Only the
public APIs should be imported as follows:

```haskell
import Synfini.Keccak (keccak256)
```

## Run unit tests

Build the library, then change directory into `test` before running the tests. For example, from the repository root
run:

```bash
cd main
daml build
cd ../test
daml test
```

## Limitations

The implementation is not yet optimized for performance. The Daml standard library does not currently support bitwise
logical operations which are necessary for the keccak hash function. These have been written by hand within this
library. Efficient standard library of these operations may make this implementation simpler and more performant.
