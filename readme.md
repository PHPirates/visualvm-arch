At the moment of writing, the visualvm package version in Arch is 1.4.4, the one in this repo at least 2.1, but the package maintainers do not respond to requests to update.

```
git clone git@github.com:PHPirates/visualvm-arch.git
cd visualvm-arch
makepkg -si
```

**Updating the package version in this repo**:

* Update the version in PKGBUILD, say 2.1
* `wget https://github.com/visualvm/visualvm.src/releases/download/2.1/visualvm_21.zip`
* `sha256sum visualvm_21.zip` and update the first checksum in PKGBUILD
