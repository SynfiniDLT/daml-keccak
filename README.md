# daml-keccak

    Copyright (c) 2023, ASX Operations Pty Ltd. All rights reserved.
    SPDX-License-Identifier: Apache-2.0

Daml library containing an implementation of the Keccak hash function. Although SHA-3 is also part of the Keccak family,
this version is not compatible with SHA-3 due to changes made in the SHA-3 standard.

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

The `keccak256` function has type `Text -> Text`, and returns the hash of the UTF-8 bytes of the `Text` in hex-encoded
form (in lowercase letters). This input/output format is the same as the built-in `sha256` function.

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

The implementation is not yet optimized for performance. The Daml standard library does not currently support bit-level
operations on integers (such as bit shifting, bit-wise and/or etc.). These are necessary for the keccak hash function.
This library implements these operations using basic arithmetic which presents a bottleneck. Having access to native
bit-level operations may provide a significant performance improvement.
