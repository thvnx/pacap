A MLIR-based Ada Parser
--

At the moment, this is just an out-of-tree build of the first MLIR toy example
you can found in `llvm-project/mlir/examples/toy/Ch1`.

# An out-of-tree build

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

```
mkdir build && cd build
cmake -G Ninja .. -DMLIR_DIR=../llvm-project-prefix/lib/cmake/mlir \
    -DLLVM_EXTERNAL_LIT=../llvm-project-build/bin/llvm-lit
cmake --build . --target toyc-ch1
```

# Sources

- https://mlir.llvm.org/getting_started/
- https://github.com/llvm/llvm-project/tree/main/mlir/examples
