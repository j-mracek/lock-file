# Image build

```podman build .```

## Container file
```
FROM ubi9/ubi:9.2-755.1697625012
RUN dnf install -y git
```

# Creating of lockfile

## Locking `git`

```podman run <ImageID> dnf -q repoquery --installed git > lock-file.txt```

## Locking direct depenencies of `git`

```podman run <ImageID> dnf -q repoquery --installed git --requires --resolve >> lock-file.txt```

## Locking all dependencies of `git`

```podman run <ImageID> dnf -q repoquery --installed git --requires --resolve --recursive >> lock-file.txt```

# Image build with lock-file

It is required to import lock-file to the image. The example uses a simple copy from local project, but it can be
replaced by file download. The workflow is functional even when lock-file is empty => the same Container file can be
used for initial build.

```podman build install-lock-file/```

## Container file

```
FROM ubi9/ubi:9.2-755.1697625012
COPY lock-file.txt /tmp/lock-file.txt
RUN dnf install -y git $(cat /tmp/lock-file.txt)
```
