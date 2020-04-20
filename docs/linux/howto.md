# howtos

## check which distribution

```bash
cat /etc/*-release
```

## install from insecure repo source(without a release file)

Sometimes

```plain
The repository 'https://storage.googleapis.com/download.dartlang.org/linux/debian unstable Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

Set the `allow-insecure` will bypass the `apt-secure` warning.

In the sources list file:

```deb
deb [allow-insecure arch=amd64] ...
```
