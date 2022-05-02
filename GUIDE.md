# Compile Guide

Hint: following guide is tested on Ubuntu 20.04 LTS WSL2 version.

1. clone from repo:

```shell
git clone <git@repo.path>
cd mitsuba_ubuntu20
```

2. copy one of the following file to the main directory and rename it to 'config.py'

`build/config-linux-gcc.py`

`build/config-linux-gcc-debug.py`

(`-fPIC` and `-std=gnu++11` options were added into compile flags)

3. install dependencies by using `apt`:

```shell
sudo apt-get install build-essential libpng-dev libjpeg-dev libilmbase-dev libxerces-c-dev libboost-all-dev libopenexr-dev libglewmx-dev libxxf86vm-dev libeigen3-dev libfftw3-dev
sudo apt-get install libcollada-dom-dev
sudo apt-get install qt5-default libqt5opengl5-dev libqt5xmlpatterns5-dev
```
4. create conda environment of `python2.7`:

```shell
conda create -n mtsenv python=2.7
conda activate mtsenv
```

(Hint: I don't have python 2.7 installed on my system. So I select to use `miniconda` for convenience.)

(Hint: guide to install miniconda on Linux: https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html)

5. install `scons`

```
conda install -c conda-forge scons
```

6. (Skip this step. This step has been done if this branch is used) modify following two file for using Qt5:

`data/scons/qt5.py`

`src/mtsgui/SConscript`

(Qt5*.pc files can be found at `/usr/lib/x86_64-linux-gnu/pkgconfig`)

(Reference: https://github.com/mitsuba-renderer/mitsuba/issues/32)

7. construct project:

```shell
scons -j8
```

8. (optional) set path:

```shell
source setpath.sh
```

9. (optional) test running

```shell
mtsgui
```

(Hint: If `qt.qpa.xcb: could not connect to display ` error occurred, try to update wsl version (to the version which support wslg). https://github.com/microsoft/wslg)

## Reference

https://medium.com/@sree_here/10-steps-to-install-mitsuba-renderer-on-ubuntu-38a9318fbcdf

https://gist.github.com/mlagunas/5bd92a6ef48ff18d82b22aed367d9d1c

