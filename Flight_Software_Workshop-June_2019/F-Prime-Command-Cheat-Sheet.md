# F Prime Command Cheat Sheet

This is intended to be q quick reference for F prime commands needed for completeing the FSW workshop.  Further commands can be found
in the F prime documentation and raspberry PI example.

## Setup and Implementation Commands

This section will cover commands that help setup the F prime build system, setup a new F prime module, and aid in implementation of F
prime components.

### Setup/Refresh Make System

When a new module is created, has a `mod.mk` and `Maakefile`, and has been added to `mk/config/modules.modules.mk` the build system needs
to be regenerated. This is done with the following command run from any directory that has a `mod.mk` and `Makefile` specified.

```
make gen_make
```

### Make Implementation Templates

When implementing components, templates can be generated to ease development. The following command can be run from any component
directory where the *Ai.xml* has been added to the `mod.mk` of the component and `make gen_make` has been rerun.  This command will
output *MODULE.cpp_template* and *MODULE.hpp_template* files in the directory. These can be filled in by the developer.

```
cd <component directory>
make impl
```

### Make Unit Test Files

Like the `make impl` command above, it is nice to be able to auto-generate the files required for unit testing. This can be done by
tunning the command below. It has the same requirments as the `make impl` command above.

```
cd <component directory>
make testcomp
```

## Build Commands for Linux

This section describes the commands used to build on linux. This is useful for development.

### Building and Rebuilding

These two commands can be used in component and deployment directories to build the code. The rebuild variant also runs `clean` and
`gen_make` in order to ensure that all parts of the system ar up-to-date.

```
cd <component or topology>
make # To re-generate autocode output and build code
make rebuild # To clean, generate make system, and build code
```

## Build Commands Raspberry PI

Once the user has a complete deployment ready for running on the raspberry PI, the following command can be used to rebuild 
and generate a binary ready to run on the Raspberry PI. It is recommended to always rebuild completely for this stage. 

```
cd <raspberry PI deployment dir>
make rebuild_rpi_cross
```

**Note:** this performs a cross-compile for the raspberry PI's architecture.

## Other Raspberry PI Commands

This section includes command useful for interacting with the Raspberry PI for the purposes of the FSW workshop.

### Copying the Binary to the Rasbperry PI

Copying the binary to the raspberry pi can be done via the `scp` command. It depends on the user having built the deployment
using the `make rebuild_rpi_cross` command above.

```
cd <raspberry PI deployment dir>
cp ./raspian-raspian-arm-debug-gnu-bin/<deployment name> pi@<team's pi IP>:
```

### Running Against the F Prime Ground System

Running the RPI app against thr ground system requires starting the ground system at a know network location, and pointing
the binary at that ground system.

**On Development PC**
```
cd fprime/RPI
./scripts/run_rpi_cross.sh --dictionary <path-to-deployment>/py_dict -p <team's port>
```

**On Raspbery PI Via SSH
```
./<deployment name> -a 192.168.2.2 -p <team's port>
```
