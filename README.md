# Packages
Some scripts for building ancillary convenience packages used in various projects.
The packages and package building scripts are all unofficial, but may be useful to
speedup or test projects that depend on them.

## Prebuilt Binaries
Prebuild binary packages are stored in Git LFS:
  * 

## Dependencies
These package building scripts rely rely on FPM:
  * https://github.com/jordansissel/fpm

## Package List
  * OpenFst v1.4.1 (Xenial)
  * OpenFst v1.5.1 (Xenial)
  * OpenFst v1.6.1 (Xenial)
  * OpenFst v1.6.2 (Xenial)

## Build
The supported packages can be rebuilt from scratch using the included scripts,
assuming that FPM has been installed, along with the required distribution-specific
package building tools.  See FPM for details on said dependencies.

```bash
$ cd Ubuntu-16.04/openfst-1.6.2-pkg/
$ make deb
 ...
 ...
$ ls -1 ../*deb
 openfst_1.6.2_amd64-xenial.deb
$ sudo dpkg -i ../openfst_1.6.2_amd64-xenial.deb
 ...
```

