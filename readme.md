# Dockerfiles
This repository hosts our Dockerfiles.

## RTU Compiler
The RTUs right now are raspberry Pis, and RPis don't compile Rust very well due to their low memory and CPU power. The [`Dockerfile`](rtu-compiler/Dockerfile) in the `rtu-compiler/` directory is the source for [`navasotabrewing/bcs-rtu-compiler`](https://hub.docker.com/r/navasotabrewing/bcs-rtu-compiler) on Dockerhub.

### Cross compiling for RTUs
You can use [`cross`](https://github.com/rust-embedded/cross) to cross compile Rust easily, using our Docker container.

The only rust packages in our organization that run on RTUs are [`NavasotaBrewing/cli`](https://github.com/NavasotaBrewing/cli) and [`NavasotaBrewing/network`](https://github.com/NavasotaBrewing/network). For both projects, be sure the `Cross.toml` is present with the following

```toml
# Cross.toml
[target.armv7-unknown-linux-gnueabihf]
# You may want to update this to the latest version, if available
image = "navasotabrewing/bcs-rtu-compiler:1.0.0"
```

then run
```
$ cross build --target armv7-unknown-linux-gnueabihf
```

The compiled binary will be in the `target/` directory, you can send it over to the RTUs.