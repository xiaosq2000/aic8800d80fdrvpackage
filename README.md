# aic8800d80fdrvpackage

Unofficial Linux driver for aic8800d80f (TP-LINK TL-XDN7000 wireless adaptor).

The package fixes the compile errors that stop the official driver from building
on Linux kernel 6.x and 7.x.

- v0.0.12.8(Not tested, but highly suggested): Based on official driver version 20260224.
- v0.0.10(Not tested): Based on official driver version 20250319.
- v0.0.3(Tested, not stable with some noticeable bugs): Based on official driver version 20240202.

Tested on Raspberry PI 3B+ & TP-LINK TL-XDN7000 wireless adaptor.

## Kernel support

The official driver only builds on older kernels, so the repository carries
fixes for the API changes made in 6.7, 6.11, 6.12, and in the range from 6.13 to
7.0. If you are on a kernel between 6.13 and 6.17, you need the 7.0 fix as well.
The same API changes broke the 6.13 to 6.17 range first.

The 7.0 fix was built and load tested on 7.0.0-30-generic, which is kernel
7.0.12 on x86_64. Both modules load, and the wireless device registers. The
interface connects to an access point.

## Build from source

```
git clone https://github.com/MXWXZ/aic8800d80fdrvpackage.git
rm -rf aic8800d80fdrvpackage/.git aic8800d80fdrvpackage/LICENSE aic8800d80fdrvpackage/README.md
dpkg -b aic8800d80fdrvpackage/ .
dpkg -i aic8800d80fdrvpackage_0.0.12.8_all.deb
```

## Download pre-built file

Get pre-built file from [release](https://github.com/MXWXZ/aic8800d80fdrvpackage/releases).

```
dpkg -i aic8800d80fdrvpackage_0.0.12.8_all.deb
```

## Kernel upgrades

The modules are built and installed through DKMS, so apt rebuilds them for every
new kernel it installs. `dkms` and `build-essential` are declared as package
dependencies. `dpkg -i` does not resolve dependencies, so run `apt install -f`
afterwards if they are not already present.

To check which kernels the driver is built for:

```
dkms status -m aic8800
```

The package builds for every installed kernel that has headers, not only the
running one. If a later kernel changes an API this driver has not caught up
with, that build fails loudly during the upgrade while the modules for the
earlier kernels stay in place, so booting the previous kernel still gives you a
network to fix it from. The build log is at:

```
/var/lib/dkms/aic8800/<version>/<kernel>/<arch>/log/make.log
```
