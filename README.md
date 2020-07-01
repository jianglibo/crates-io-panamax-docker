# crates-io-panamax-docker

crates io mirror docker image.

<https://github.com/k3d3/panamax>

```bash
# run image once for coping out initialized mirror directory.
docker run --name ttt jianglibo/panamax:v1.0.6 /bin/bash
docker cp ttt:/my-mirror /home/crates-mirror-root/
docker rm ttt

# sync mirror, can be called from crontab to keep synced.
docker run -v /home/crates-mirror-root/my-mirror:/my-mirror --name crates-mirror --rm jianglibo/panamax:v1.0.6
```

```bash
# for test.
* * * * *  sleep 30; /usr/bin/docker run -v /home/crates-mirror-root/my-mirror:/my-mirror --name crates-mirror --rm jianglibo/panamax:v1.0.6 echo hello >> /home/mirror-sync.log 2>&1

# daily sync.
@daily /usr/bin/docker run -v /home/crates-mirror-root/my-mirror:/my-mirror --name crates-mirror --rm jianglibo/panamax:v1.0.6 >> /home/mirror-sync.log 2>&1

```

## an available crates mirror for you

### Setting environment variables

In order to ensure `rustup` knows where to look for the Rust components, we need to set some environment variables. Assuming the mirror is hosted at <http://panamax.internal/>:

```bash
export RUSTUP_DIST_SERVER=https://crates.fh.gov.cn
export RUSTUP_UPDATE_ROOT=https://crates.fh.gov.cn/rustup
```

These need to be set whenever `rustup` is used, so these should be added to your `.bashrc` file (or equivalent).

### Installing `rustup`

If you already have `rustup` installed, this step isn't necessary, however if you don't have access to <https://rustup.rs>, the mirror also contains the `rustup-init` files needed to install `rustup`.

Assuming the mirror is hosted at <https://crates.fh.gov.cn/>, you will find the `rustup-init` files at <https://crates.fh.gov.cn/rustup/dist/>. The `rustup-init` file you want depends on your architecture. Assuming you're running desktop Linux on a 64-bit machine:

```bash
wget https://crates.fh.gov.cn/rustup/dist/x86_64-unknown-linux-gnu/rustup-init
chmod +x rustup-init
./rustup-init
```

This will let you install `rustup` the similarly following the steps from <https://rustup.rs>. This will also let you use `rustup` to keep your Rust installation updated in the future.

### Configuring `cargo`

`Cargo` also needs to be configured to point to the mirror. This can be done by adding the following lines to `~/.cargo/config` (creating the file if it doesn't exist):

```toml
[source.my-mirror]
registry = "https://crates.fh.gov.cn/crates.io-index"
[source.crates-io]
replace-with = "my-mirror"
```
