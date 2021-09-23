
# PKGBUILD-MACOSX
#### Arch Linux (pacman)style PKGBUILD files for macosx
now, it can only to build universal(arm64,x86_64) pkg, mkpkg need more work to improve.
## how to use
0. install Xcode
1. make some necessary directories in "/usr/local"
```sh
bin/init_dirs
```
2. cp `pkgconfig-macosx` to `/usr/local/share/pkgconfig`
```sh
cp -a pkgconfig-macosx/ /usr/local/share/pkgconfig
```
3. build `pkg-config` first before starting to build others
```sh
bin/mkpkg PKGBUILD/pkg-config.PKGBUILD
```
now build them all one by one
```sh
bin/mkpkg PKGBUILD/<any.PKGBUILD>
```
......

all builded pakages are in the `PKGROOT` dir.
