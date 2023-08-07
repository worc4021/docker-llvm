# syntax=docker/dockerfile-upstream:master-labs

ARG DEBIAN_VERSION=stable-slim
ARG LLVM_VERSION=16.0.0
FROM debian:${DEBIAN_VERSION}

RUN apt update && \
    apt install -y \
        curl gnupg lsb-release \
        gdb cmake libboost-all-dev gawk python3 pip \
        pkg-config libeigen3-dev ninja-build \
        gcc-12 g++-12 

ADD https://github.com/llvm/llvm-project.git#llvmorg-${LLVM_VERSION} /llvm

RUN cmake -S /llvm/llvm -B /llvm/build \
    -DLLVM_ENABLE_PROJECTS="clang" -DLLVM_ENABLE_RUNTIMES="libcxx;libcxxabi" \
    -DCMAKE_BUILD_TYPE=Release -G ninja && \
    cmake --build /llvm/build --target install