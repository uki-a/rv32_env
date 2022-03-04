# rv32_env
RV32GC compiling environment using Docker

After installing [Docker](https://www.docker.com/), run the command to build the image.
This will take a long time.

```
docker build -t ubuntu/rv32:1.0 .
```

Then build the container.
```
docker run -it ubuntu/rv32:1.0
```
