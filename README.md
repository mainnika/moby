# moby engine

This fork contains the patch to force use archive package with the «user namespace» option.
Since dev-node files are not commonly used in docker images this change doesn't broke the compatibility.

## initial issue

The systemd-nspawnd allows you to run dockerd in the virtualized environment, but with specific restrictions.
The user is restricted to create dev-node files even if nspawn configuration has all capabilities. Then if the docker image has dev-node files dockerd will not be able to run this image.

e.g. `ubuntu:16.04`

```
[root@localhost ~]# docker run --rm -it ubuntu:16.04 bash
Unable to find image 'ubuntu:16.04' locally
16.04: Pulling from library/ubuntu
fe703b657a32: Extracting [==================================================>]  44.19MB/44.19MB
f9df1fafd224: Download complete
a645a4b887f9: Download complete
57db7fe0b522: Download complete
docker: failed to register layer: Error processing tar file(exit status 1): operation not permitted.
See 'docker run --help'.
```

## ready-to-use branch

- 18.09