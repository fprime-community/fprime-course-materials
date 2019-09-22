# F Prime Command Cheat Sheet

This is intended to be q quick reference for F prime commands needed for completeing the FSW workshop.  Further commands can be found
in the F prime documentation and raspberry PI example.

## Tutorial Example

https://github.com/timcanham/fprime/tree/tutorial/RobotArm

## Development Process Notes

[Development-Process.md](Development-Process.md)

## Setup and Implementation Commands

This section will cover commands that help setup the F prime build system, setup a new F prime module, and aid in implementation of F
prime components.

### Setup/Refresh Make System

When a new module is created, has a `CMakeLists.txt`, and has been added to a parent's `CMakeLists.txt` using `add_fprime_subdirectory()`. Once done, rerun cmake in the build directory, or make in the build directory to trigger a cmake refresh.

### Make Implementation Templates

When implementing components, templates can be generated to ease development. The following command can be run from any component
directory where the *Ai.xml* has been created. No build system dependency is required. These can be copied to new files and filled in by the developer.

```
cd <component directory>
<fprime>/Autocoders/Python/bin/impl.py -b <path/to/BUILD_ROOT> *Ai.xml
```

## Build Commands for Linux

This section describes the commands used to build on linux. This is useful for development.

### Building and Rebuilding

Building requires and empty directory to be used by cmake.  Rebuilding requires running `make` in that subdirectory.

```
mkdir build-linux
cd build-linux
cmake <path/to/deployment>
make # To build or rebuild
```

## Build Commands Raspberry PI

Once the user has a complete deployment ready for running on the raspberry PI, the following command can be used to rebuild 
and generate a binary ready to run on the Raspberry PI. This is similar to Linux, but supplies a toolchain file to CMake in order
to build for Raspberry Pi.

```
mkdir build-rpi
cd build-rpi
cmake <path/to/rpi deployment> -DCMAKE_TOOLCHAIN_FILE=<path/to/fprime>/cmake/toolchain/arm-linux-gnueabihf.cmake
make
make install
```

**Note:** this performs a cross-compile for the raspberry PI's architecture.

## Other Raspberry PI Commands

This section includes command useful for interacting with the Raspberry PI for the purposes of the FSW workshop.

### Copying the Binary to the Rasbperry PI

Copying the binary to the raspberry pi can be done via the `scp` command. It depends on the user having built the deployment
using the `make rebuild_rpi_cross` command above.

```
cd <raspberry PI deployment dir>
scp ./bin/arm-linux-gnueabihf/<deployment name> pi@<team's pi IP>:
```

### Running Against the F Prime Ground System

Running the RPI app against thr ground system requires starting the ground system at a know network location, and pointing
the binary at that ground system.

**On Development PC**
```
cd fprime/
./Gds/bin/run_deployment.sh -d <path/to/deployment> -n -p <team's port> -g html
```

**On Raspbery PI Via SSH**
```
./<deployment name> -a <address of ground station> -p <team's port>
```
