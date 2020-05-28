# mergerfs

<img src="https://raw.githubusercontent.com/hotio/docker-mergerfs/master/img/mergerfs.png" alt="Logo" height="130" width="130">

![Base](https://img.shields.io/badge/base-alpine-blue)
[![GitHub](https://img.shields.io/badge/source-github-lightgrey)](https://github.com/hotio/docker-mergerfs)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/mergerfs)](https://hub.docker.com/r/hotio/mergerfs)
[![Discord](https://img.shields.io/discord/610068305893523457?color=738ad6&label=discord&logo=discord&logoColor=white)](https://discord.gg/3SnkuKp)
[![Upstream](https://img.shields.io/badge/upstream-project-yellow)](https://github.com/trapexit/mergerfs)

## Starting the container

Just the basics to get the container running:

```shell
docker run --rm hotio/mergerfs ...
```

The default `ENTRYPOINT` is `mergerfs -f`.

## Tags

| Tag      | Description                    | Build Status                                                                                                                                                | Last Updated                                                                                                                                                          |
| ---------|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| latest   | The same as `stable`           |                                                                                                                                                             |                                                                                                                                                                       |
| stable   | Stable version                 | [![Build Status](https://cloud.drone.io/api/badges/hotio/docker-mergerfs/status.svg?ref=refs/heads/stable)](https://cloud.drone.io/hotio/docker-mergerfs)   | [![GitHub last commit (branch)](https://img.shields.io/github/last-commit/hotio/docker-mergerfs/stable)](https://github.com/hotio/docker-mergerfs/commits/stable)     |
| unstable | Every commit to master branch  | [![Build Status](https://cloud.drone.io/api/badges/hotio/docker-mergerfs/status.svg?ref=refs/heads/unstable)](https://cloud.drone.io/hotio/docker-mergerfs) | [![GitHub last commit (branch)](https://img.shields.io/github/last-commit/hotio/docker-mergerfs/unstable)](https://github.com/hotio/docker-mergerfs/commits/unstable) |

You can also find tags that reference a commit or version number.

## Using the mergerfs mount on the host

By setting the `bind-propagation` to `shared` on the volume `mountpoint`, like this `-v /data/mountpoint:/mountpoint:shared`, you are able to access the mount from the host. If you want to use this mount in another container, the best solution is to create a volume on the parent folder of that mount with `bind-propagation` set to `slave`. For example, `-v /data:/data:slave` (`/data` on the host, would contain the previously created volume `mountpoint`). Doing it like this will ensure that when the container creating the mount restarts, the other containers using that mount will recover and keep working.

## Extra docker privileges

In most cases you will need some or all of the following flags added to your command to get the required docker privileges when using a mergerfs mount.

```shell
--security-opt apparmor:unconfined --cap-add SYS_ADMIN --device /dev/fuse
```
