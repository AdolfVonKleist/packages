# Packages
Some scripts for building ancillary convenience packages used in various projects.
The packages and package building scripts are all unofficial, but may be useful to
speedup or test projects that depend on them.

## Prebuilt Binaries
Prebuild binary packages are stored in Git LFS and will not be downloaded on checkout
by default. To download a specific debian package:
```bash
# Checkout the repository
$ git clone https://github.com/AdolfVonKleist/packages.git
$ cd packages/
# Retrieve the binary from Git LFS
$ git lfs fetch --exclude "" --include Ubuntu-16.04/debs/openfst_1.6.2_amd64-xenial.deb
$ git lfs checkout Ubuntu-16.04/debs/openfst_1.6.2_amd64-xenial.deb
# Install the package
$ sudo dpkg -i Ubuntu-16.04/debs/openfst_1.6.2_amd64-xenial.deb
 ...
```

## Dependencies
These package building scripts rely on FPM for package scripting:
  * https://github.com/jordansissel/fpm

## Package List
### OpenFst
OpenFst packages are compiled with all available core extensions.  See the individual Makefiles for details.
Note that 'core extensions' does not include the Python bindings (```--enable-python```).
  * [OpenFst v1.4.1](http://www.openfst.org/twiki/pub/FST/FstDownload/openfst-1.4.1.tar.gz) (Xenial)
  * [OpenFst v1.5.1](http://www.openfst.org/twiki/pub/FST/FstDownload/openfst-1.5.1.tar.gz) (Xenial)
  * [OpenFst v1.6.1](http://www.openfst.org/twiki/pub/FST/FstDownload/openfst-1.6.1.tar.gz) (Xenial)
  * [OpenFst v1.6.2](http://www.openfst.org/twiki/pub/FST/FstDownload/openfst-1.6.2.tar.gz) (Xenial)

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

