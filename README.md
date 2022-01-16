<!-- omit in toc -->
# The WRF-TEB software repository

The coupled WRF-TEB ([Meyer et al., 2020a](https://doi.org/10.1029/2019MS001961)) couples the single layer Town Energy Balance (TEB; [Masson, 2000](https://doi.org/10.1023/A:1002463829265)) software ([Meyer et al., 2020b](https://doi.org/10.21105/joss.02008)) to the Weather Research and Forecasting (WRF; [Skamarock et al., 2019](https://doi.org/10.5065/1dfh-6p97)) software with CMake support ([Riechert & Meyer, 2021](https://doi.org/10.21105/joss.01468)).

<!-- omit in toc -->
## Contents
- [Installation](#installation)
- [Usage](#usage)
- [How to cite](#how-to-cite)
- [Copyright and license](#copyright-and-license)


## Installation

WRF-TEB is built with [WRF-CMake](https://github.com/WRF-CMake/wrf) and [TEB](https://github.com/teb-model/teb). Software releases are available from the [WRF-TEB release page](https://github.com/TEB-model/wrf-teb/releases). For standard installation on Linux use:

```sh
cd wrf-teb
mkdir build && cd build

cmake -GNinja -DCMAKE_BUILD_TYPE=Release \
      -DMODE=dmpar \
      -DCMAKE_INSTALL_PREFIX=install ..

# https://ninja-build.org/
ninja install # -j <nproc>
```

**Notes**: the TEB software version is defined using the `GIT_TAG` variable in `external/teb/CMakeLists.txt`. To specify the location to TEB use the `TEB_DIR` flag (e.g. `-DTEB_DIR=path/to/teb/dir`). For a list of required software dependencies see [doc/cmake/INSTALL.md#install-dependencies](doc/cmake/INSTALL.md#install-dependencies). For advanced build and install information see [doc/cmake/INSTALL.md#build-and-install-wrf-cmake](doc/cmake/INSTALL.md#build-and-install-wrf-cmake).


## Usage

Standard [WRF documentation](https://www2.mmm.ucar.edu/wrf/users/docs/user_guide_v4/contents.html) applies. To run a case using WRF-TEB, enable TEB from the `namelist.input` with `sf_urban_physics = 4` and rename `URBPARM_TEB.TBL` to `URBPARM.TBL`. Make sure to change options and parameter values to match those for case study. See the [namelist option page in TEB](https://github.com/TEB-model/teb/blob/master/docs/namelist-options.md) for more information.


## How to cite

Please cite WRF-TEB and WRF-CMake with the following DOIs:

- WRF-TEB: https://doi.org/10.1029/2019MS001961
- WRF-CMake: https://doi.org/10.21105/joss.01468

Additional, version-specific DOIs are available on Zendo at https://doi.org/10.5281/zenodo.3898327 and https://doi.org/10.5281/zenodo.3403342 for WRF-TEB and WRF-CMake, respectively. 


## Copyright and license

General WRF copyright and license applies for any files part of the original WRF distribution -- see the [README](README) file for more details.

WRF-CMake source files are licensed under the MIT license and marked as:

```
WRF-CMake (https://github.com/WRF-CMake/wrf).
Copyright <year> M. Riechert and D. Meyer. Licensed under the MIT License.
```

WRF-TEB source files are licensed under the MIT license and marked as:

```
WRF-TEB (https://github.com/teb-model/wrf-teb).
Copyright <year> D. Meyer. Licensed under the MIT License.
```
