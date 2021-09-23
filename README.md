
# PKGBUILD-MACOSX
#### Arch Linux (pacman)style PKGBUILD files for macosx
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
