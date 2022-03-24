# rv32_env
### RV32GC compiling environment using Docker

The environment supports RV32GC instruction set and consists of the followings.
- RISC-V GNU Cross-compiler (along with riscv-gnu-toolchain repository)
- Spike compiler
- riscv-pk compiler

Of course, you can recompile them to support the combination of other instruction sets.

# How to build

After installing [Docker](https://www.docker.com/), run the command to build the image.
This will take a while.

```
cd rv32
docker build -t ubuntu/rv32:1.0 .
```

Then build the container.
```
docker run -it ubuntu/rv32:1.0
```
