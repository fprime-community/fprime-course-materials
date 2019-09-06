This file seeks to give a quick reference for the development process used for the FSW workshop.

# Setting Up a CMake Build

In order to build code, we will be using CMake. This means builds are typically done in a separate
directory from source.  We can set one up quickly.

```
mkdir build
cmake <path/to/deployment>
make  <target or empty>
```

# Ports

In order to add new ports into the system follow the following steps.

**Note:** adding files below is easiest by copying from an existing port and editing it.

1. Create a new port directory 
2. Create a port `*Ai.xml` file and fill it out
3. Add `CMakeLists.txt` by ensuring the port's `*Ai.xml` is listed in `SOURCE_FILES`
4. Add port directory to the Deployment's `CMakeLists.txt`
5. (In CMake Build Directory) `make <port target name i.e. RobotArm_I2cPort>`

# Components

**Note:** adding files below is easiest by copying from an existing component and editing it.

1. Create a new component directory 
2. Create a component `*Ai.xml` file and fill it out
3. Run `<fprime>/Autocoders/Python/bin/implgen.py -b <Path to BUILD_ROOT> <path to Ai.xml>`
4. Rename the generated `*-template` files to remove the `-template` suffix
5. Add `CMakeLists.txt` by ensuring the components's `*Ai.xml` and `*Impl.cpp` is listed in `SOURCE_FILES`
6. Add component directory to the Deployment's `CMakeLists.txt`
7. (In CMake Build Directory) `make <port target name i.e. RobotArm_I2cPort>`


# Deployments

1. Create a `Top` topology directory. This contains `Main.cpp` and other files.
2. Create a Deployment CMakeLists.txt file, including all components and ports using `add_fprime_subdirectory`.
3. (In CMake Build Directory) `make`
