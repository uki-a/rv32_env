FROM ubuntu:18.04

LABEL version="1.0"
LABEL description="RV32GC 開発環境"

WORKDIR /tmp/

RUN apt -y update
RUN apt -y install git autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev

RUN git clone --recursive https://github.com/riscv-collab/riscv-gnu-toolchain.git
ENV RV32 /opt/rv32gc
RUN cd riscv-gnu-toolchain && \
    mkdir build && cd build && \
    ../configure --prefix=$RV32 --with-arch=rv32gc --with-abi=ilp32d && \
    make -j$(nproc) && \
    cd ../../

RUN apt install device-tree-compiler
RUN git clone https://github.com/riscv-software-src/riscv-isa-sim.git
RUN cd riscv-isa-sim && \
    mkdir build && cd build && \
    ../configure --prefix=$RV32 --with-isa=rv32gc && \
    make && \
    make install

RUN git clone https://github.com/riscv-software-src/riscv-pk.git
RUN cd riscv-pk && \
    mkdir build && cd build && \
    ../configure --prefix=$RV32 --host=riscv32-unknown-elf && \
    make && \
    make install

RUN echo 'export PATH=$PATH:$RV32/bin:$RV32/riscv32-unknown-elf' >> ~/.bashrc

RUN cd /work
RUN echo '#include <stdio.h>

CMD ["/bin/bash"]
