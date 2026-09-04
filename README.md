# aic8800d80fdrvpackage

Unofficial Linux driver for aic8800d80f (TP-LINK TL-XDN7000 wireless adaptor).

Fix compile error on Linux kernel version 6.x. 

- v0.0.10(Not tested, but highly suggested): Based on official driver version 20250319.
- v0.0.3(Tested, not stable with some noticeable bugs): Based on official driver version 20240202.

Tested on Raspberry PI 3B+ & TP-LINK TL-XDN7000 wireless adaptor.

## Build from source

```
git clone https://github.com/MXWXZ/aic8800d80fdrvpackage.git
rm -rf aic8800d80fdrvpackage/.git aic8800d80fdrvpackage/LICENSE aic8800d80fdrvpackage/README.md
dpkg -b aic8800d80fdrvpackage/ .
dpkg -i aic8800d80fdrvpackage_0.0.10_all.deb
```

## Download pre-built file

Get pre-built file from [release](https://github.com/MXWXZ/aic8800d80fdrvpackage/releases).

```
dpkg -i aic8800d80fdrvpackage_0.0.10_all.deb
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
