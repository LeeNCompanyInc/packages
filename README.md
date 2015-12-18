openwrt-packages
================

Various packages does not come with OpenWrt default feeds

## How to Install

```
cp feeds.conf.default feeds.conf
echo "src-git https://github.com/LeeNCompanyInc/packages.git" >> feeds.conf
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make
```

#### n2n_v2

* Makefile from: http://pastebin.com/AUKXbuzr
* n2n_v2.init and config from: https://dev.openwrt.org/attachment/ticket/10069/packages_update_to_n2n_v2.patch
