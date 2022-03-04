FROM ubuntu:18.04

LABEL version="1.0"
LABEL description="RV32GC Compiler Environment"

WORKDIR /tmp/

SHELL ["/bin/bash", "-c"]

RUN apt -y update
RUN apt -y install git autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev

RUN git clone --recursive https://github.com/riscv-collab/riscv-gnu-toolchain.git
ENV RV32 /opt/rv32gc
RUN cd riscv-gnu-toolchain && \
    mkdir build && cd build && \
    ../configure --prefix=$RV32/cross --with-arch=rv32gc --with-abi=ilp32d && \
    make -j$(nproc) && \
    cd ../../

RUN echo 'export PATH=$PATH:$RV32/cross/bin' >> ~/.bashrc && source ~/.bashrc
RUN export PATH=$PATH:$RV32/cross/bin

RUN apt install device-tree-compiler
RUN git clone https://github.com/riscv-software-src/riscv-isa-sim.git
RUN cd riscv-isa-sim && \
    mkdir build && cd build && \
    ../configure --prefix=$RV32/spike --with-isa=rv32gc && \
    make && \
    make install && \
    cd ../../
RUN export PATH=$PATH:$RV32/spike/bin

RUN git clone https://github.com/riscv-software-src/riscv-pk.git
RUN cd riscv-pk && \
    git reset --hard 423801e35d048187d88fcbff55e20c4c34d27bee && \
    mkdir build && cd build && \
    export PATH=$PATH:$RV32/cross/bin && \
    ../configure --prefix=$RV32/pk --host=riscv32-unknown-elf && \
    make && \
    make install
RUN export PATH=$PATH:$RV32/pk/riscv32-unknown-elf/bin

RUN echo 'export PATH=$PATH:$RV32/riscv32-unknown-elf' >> ~/.bashrc && source ~/.bashrc

RUN mkdir /workdir && cd /workdir
RUN echo 'Hello, World'
