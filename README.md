A MLIR-based Ada Parser
--

At the moment, this is just an out-of-tree build of the first MLIR toy example
you can find in: `llvm-project/mlir/examples/toy/Ch1`.

# An out-of-tree build

## Using development packages (prefered way)

Get the packages (example for Ubuntu 20.04), see https://apt.llvm.org/:

```sh
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
sudo add-apt-repository 'deb http://apt.llvm.org/focal/ llvm-toolchain-focal main'
sudo apt-get install clang-16 lldb-16 lld-16
sudo apt-get install libllvm-16-ocaml-dev libllvm16 llvm-16 llvm-16-dev llvm-16-doc llvm-16-examples llvm-16-runtime
sudo apt-get install libmlir-16-dev mlir-16-tools
```

Configure and build this parser with:

```sh
mkdir build && cd build
cmake -G Ninja .. -DMLIR_DIR=/usr/lib/llvm-16/lib/cmake/mlir \
    -DCMAKE_C_COMPILER=clang-16 -DCMAKE_CXX_COMPILER=clang++-16
cmake --build . --target toyc-ch1
```

## By building LLVM

First, build LLVM/MLIR:

```sh
cmake -G Ninja ../llvm-project/llvm \
  -DLLVM_ENABLE_PROJECTS=mlir \
  -DLLVM_BUILD_EXAMPLES=ON \
  -DLLVM_TARGETS_TO_BUILD="X86" \
  -DCMAKE_BUILD_TYPE=Release \
  -DLLVM_ENABLE_ASSERTIONS=ON \
  -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ \
  -DLLVM_ENABLE_LLD=ON \
  -DLLVM_INSTALL_UTILS=ON \
  -DCMAKE_INSTALL_PREFIX=$PREFIX/llvm-project-prefix \
  -DLLVM_OCAML_INSTALL_PATH=$PREFIX/llvm-project-prefix/lib/ocaml \
  -DLLVM_ENABLE_BINDINGS=OFF
```

Configure and build this parser with:

```sh
mkdir build && cd build
cmake -G Ninja .. -DMLIR_DIR=../llvm-project-prefix/lib/cmake/mlir \
    -DLLVM_EXTERNAL_LIT=../llvm-project-build/bin/llvm-lit
cmake --build . --target toyc-ch1
```

# Sources

- https://mlir.llvm.org/getting_started/
- https://github.com/llvm/llvm-project/tree/main/mlir/examples
