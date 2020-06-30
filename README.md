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
