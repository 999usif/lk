# Blank Slate ZMK Firmware

This repo contains the firmware for the Blank Slate PCB.

For full build guide for the Blank Slate, see https://docs.lpgala.xyz/docs/blank-slate-build-guide/overview/



# todo
- [ ] fix macros for curly braces
- [ ] fix macros for square braces
- [ ] fix macros for lt and gt

- [ ] printscreen

- [ ] get battery
- [ ] secure keyboard in case somehow (friction fit?)

- [ ] globe button for macos

# bruh
[src](https://zmk.dev/docs/development/local-toolchain/setup/native) 
## prereq
[Install dependencies section](https://docs.zephyrproject.org/4.1.0/develop/getting_started/index.html#install-dependencies) 

```
git cmake ninja-build gperf ccache dfu-util device-tree-compiler wget python3-dev python3-pip python3-setuptools python3-tk python3-wheel xz-utils file make gcc gcc-multilib g++-multilib libsdl2-dev libmagic1
```
## setup env
1. clone this repo          `git clone URL` 
2. make venv                `python -m venv .venv` 
3. source venv              `source .venv/bin/activate`
4. pip install west         `pip insatll west` 
5. init                     `west init -l lk` 
6. cd lk                    `cd lk`
7. west update              `west update` 
8. west zephyr-export       `west zephyr-export` 
9. install requirements     `pip install -r zephyr/scripts/requirements.txt` 
10. cd to home              `cd` 
11. install zephyr sdk      `wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.8/zephyr-sdk-0.16.8_linux-x86_64.tar.xz`
12. untar                   `tar xf zephyr-sdk-0.16.8_linux-x86_64.tar.xz` 
13. cd into sdk dir         `cd zephyr-sdk-0.16.8` 
14. run setup               `./setup.sh` 

## build (lpgalaxy_blank_slate)
1. cd zmk-dir               
```bash
cd <path>/lk
```
2. export env vars
```bash
export ZEPHYR_SDK_INSTALL_DIR=$HOME/zephyr-sdk-0.16.8 
export ZEPHYR_TOOLCHAIN_VARIANT=zephyr 
```
3. get old cmake3 in pip    
```bash
pip install "cmake==3.30.5"
```
4. fix setuptools build error
```bash
pip install --force-reinstall "setuptools<81"
```

## west build normal
5. west build
```bash
west build -s zmk/app -d /tmp/zmk-build -b lpgalaxy_blank_slate -- -DZMK_CONFIG=$PWD/config
```
6. rename the output uf2 file
```bash
mkdir /tmp/zmk-build/artifacts
[ -f /tmp/zmk-biuld/zephyr/zmk.uf2 ]
cp /tmp/zmk-build/zephyr/zmk.uf2 /tmp/zmk-build/artifacts/lpgalaxy_blank_slate-zmk.uf2
```

## west build studio (lpgalaxy_blank_slate-studio)
5. west build
```bash
west build -s zmk/app -d "/tmp/zmk-build" -b "lpgalaxy_blank_slate" -S "studio-rpc-usb-uart" -- -DZMK_CONFIG=$PWD/config -DCONFIG_ZMK_STUDIO=y
```
6. rename the output uf2 file
```bash
mkdir /tmp/zmk-build/artifacts
[ -f /tmp/zmk-biuld/zephyr/zmk.uf2 ]
cp /tmp/zmk-build/zephyr/zmk.uf2 /tmp/zmk-build/artifacts/lpgalaxy_blank_slate-studio.uf2
```
