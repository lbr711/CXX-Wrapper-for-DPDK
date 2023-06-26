# CXX-Wrappers-for-DPDK
## PcapPlusPlus
[PcapPlusPlus](https://pcapplusplus.github.io/docs/quickstart) provides C++ wrappers for DPDK which is a library developed by C. Owing to PcapPlusPlus, We can use C++ for the development of DPDK applications. 

## Installation
First, download and install [DPDK (version <= 21.11)](http://core.dpdk.org/download/).
For example, download the dpdk-19.11.14.tar.xz.
Here, use "make" to compile instead of "meson & ninja", avoiding the error that libs cannot be found. 
``` shell
tar xvf dpdk-19.11.14.tar.xz & cd dpdk-stable-19.11.14
make config T=x86_64-native-linuxapp-gcc
make
sudo make install
sudo ldconfig
```
Second, git clone this [repo](https://github.com/seladb/PcapPlusPlus) and install PcapPlusPlus with DPDK. Switch to the tag v22.11, then click the green button for downloading the code. Copy the HTTPS URL to git clone as below: 
``` shell
git clone https://github.com/seladb/PcapPlusPlus.git
cd PcapPlusPlus
./configure-linux.sh --dpdk --dpdk-home "Here is the absolute path to your dpdk-stable-19.11.14"
make
sudo make install
sudo ldconfig
```
