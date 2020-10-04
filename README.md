[<img src="https://hotio.dev/img/mergerfs.png" alt="logo" height="130" width="130">](https://github.com/trapexit/mergerfs)

[![GitHub Source](https://img.shields.io/badge/github-source-ffb64c?style=flat-square&logo=github&logoColor=white)](https://github.com/docker-hotio/docker-mergerfs)
[![GitHub Registry](https://img.shields.io/badge/github-registry-ffb64c?style=flat-square&logo=github&logoColor=white)](https://github.com/users/hotio/packages/container/package/mergerfs)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/mergerfs?color=ffb64c&style=flat-square&label=pulls&logo=docker&logoColor=white)](https://hub.docker.com/r/hotio/mergerfs)
[![Discord](https://img.shields.io/discord/610068305893523457?style=flat-square&color=ffb64c&label=discord&logo=discord&logoColor=white)](https://hotio.dev/discord)
[![Upstream](https://img.shields.io/badge/upstream-project-ffb64c?style=flat-square)](https://github.com/trapexit/mergerfs)
[![Website](https://img.shields.io/badge/website-hotio.dev-ffb64c?style=flat-square)](https://hotio.dev/containers/mergerfs)

## Starting the container

Just the basics to get the container running:

```shell
docker run --rm hotio/mergerfs ...
```

The default `ENTRYPOINT` is `mergerfs -f`.

## Tags

| Tag                | Upstream                      | Version | Build |
| -------------------|-------------------------------|---------|-------|
| `release` (latest) | GitHub releases               | ![version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=&query=%24.version&url=https%3A%2F%2Fraw.githubusercontent.com%2Fdocker-hotio%2Fdocker-mergerfs%2Frelease%2FVERSION.json) | ![build](https://img.shields.io/github/workflow/status/docker-hotio/docker-mergerfs/build/release?style=flat-square&label=) |
| `nightly`          | Every commit to master branch | ![version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=&query=%24.version&url=https%3A%2F%2Fraw.githubusercontent.com%2Fdocker-hotio%2Fdocker-mergerfs%2Fnightly%2FVERSION.json) | ![build](https://img.shields.io/github/workflow/status/docker-hotio/docker-mergerfs/build/nightly?style=flat-square&label=) |

You can also find tags that reference a commit or version number.

## Using the mergerfs mount on the host

By setting the `bind-propagation` to `shared` on the volume `mountpoint`, like this `-v /data/mountpoint:/mountpoint:shared`, you are able to access the mount from the host. If you want to use this mount in another container, the best solution is to create a volume on the parent folder of that mount with `bind-propagation` set to `slave`. For example, `-v /data:/data:slave` (`/data` on the host, would contain the previously created volume `mountpoint`). Doing it like this will ensure that when the container creating the mount restarts, the other containers using that mount will recover and keep working.

## Extra docker privileges

In most cases you will need some or all of the following flags added to your command to get the required docker privileges when using a mergerfs mount.

```shell
--security-opt apparmor:unconfined --cap-add SYS_ADMIN --device /dev/fuse
```
