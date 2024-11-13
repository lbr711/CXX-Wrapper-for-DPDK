# CXX-Wrapper-for-DPDK
## PcapPlusPlus
[PcapPlusPlus](https://pcapplusplus.github.io/docs/quickstart) is the C++ wrapper for DPDK. Since using PcapPlusPlus, we can use C++ to develop DPDK applications. 

## Installation
First, download and install [DPDK (version <= 21.11)](http://core.dpdk.org/download/).
For example, download the dpdk-19.11.14.tar.xz.
Here, use "make" to compile instead of "meson & ninja", avoiding the error that libs cannot be found. After the command "sudo make install", the complied dynamic libraries are installed in the directory "usr/local/lib", and the complied header files are installed in the directory "usr/local/include/dpdk". 
``` shell
tar xvf dpdk-19.11.14.tar.xz & cd dpdk-stable-19.11.14
make config T=x86_64-native-linuxapp-gcc
make
sudo make install
sudo ldconfig
```
Note that: when building some old versions of DPDK, there will appear "fallthrough" warnings, which is treated as errors after gcc 7.0. Thus we should modify the makefiles in both the directory "yourPath2dpdk/kernel/linux/kni/Makefile" and the directory "yourPath2dpdk/kernel/linux/igb_uio/Makefile". Concretely, we should add '-w' in 'CFLAGS'.

Second, git clone this [repo](https://github.com/seladb/PcapPlusPlus) and install PcapPlusPlus with DPDK. Switch to the tag v22.11, then click the green button for downloading the code. Copy the HTTPS URL to git clone as below: 
``` shell
git clone https://github.com/seladb/PcapPlusPlus.git
cd PcapPlusPlus
./configure-linux.sh --dpdk --dpdk-home "Here is the absolute path to your dpdk-stable-19.11.14 directory"
make
sudo make install
sudo ldconfig
```

## Usage
In the PcapPlusPlus directory, use the Python script called setup-dpdk.py to bind NICs to DPDK UIO drivers like igb_uio, etc. The first param can be setup, status, and restore. The three kinds of the value are for binding NICs, checking the status of NICs, and unbinding NICs, respectively.

``` shell
sudo python3 setup-dpdk.py setup -g 512 -i ens33 
sudo python3 setup-dpdk.py status
sudo python3 setup-dpdk.py restore
```

## DPDK supported NICs
Not all kinds of NICs can support DPDK, here is the [list](http://core.dpdk.org/supported/nics/) that illustrates which kinds of NICs support DPDK.
