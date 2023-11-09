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
