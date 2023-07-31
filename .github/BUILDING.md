# Building

## The dependencies for Debian-like distributions

```sh
sudo apt install build-essential cmake libunwind-dev libglfw3-dev libvulkan-dev vulkan-validationlayers-dev spirv-tools glslang-tools libspirv-cross-c-shared-dev python3-pip git
```

> git is only needed for ubuntu 22.04

## The dependencies for Fedora distributions

```sh
sudo dnf install cmake libunwind-devel glfw-devel vulkan-devel vulkan-validation-layers-devel spirv-tools glslang-devel gcc-c++ gcc spirv-tools-devel xbyak-devel python3-pip 
```

## The dependencies for Arch distributions

```sh
sudo pacman -S cmake libunwind glfw-x11 vulkan-devel glslang python-pip git cmake
```

> Side note you will need to pull ``spirv-cross`` from the AUR for now so do the following

```sh
sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si
```

```sh
yay -S spirv-cross
```

## We need one more thing

Python2 is now replaced fully and to use ```ps4_unfself``` we have to use python3 and install future using ```pip```

```sh
pip install future
```

## Getting spriv-cross on Fedora and Arch Linux

```sh
git clone https://github.com/KhronosGroup/SPIRV-Cross && cd SPIRV-Cross && mkdir build && cd build && cmake .. && cmake --build . && sudo make install
```

> **Warning**<br/>
> Fedora will compile to a point and then error out
> Arch will have to use xbyak from the aur for now

## Cloning the Repo

```sh
git clone --recursive https://github.com/RPCSX/rpcsx && cd rpcsx
```

```sh
git submodule update --init --recursive
```

## Compiling the emulator

```sh
mkdir -p build && cd build && cmake .. && cmake --build .
```

## Creating a Virtual HDD

> The PS4 has a case-insensitive filesystem. To create the Virtual HDD, do the following:

```sh
truncate -s 512M ps4-hdd.exfat

mkfs.exfat -n PS4-HDD ./ps4-hdd.exfat

mkdir ps4-fs

sudo mount -t exfat -o uid=`id -u`,gid=`id -g` ./ps4-hdd.exfat ./ps4-fs
```
