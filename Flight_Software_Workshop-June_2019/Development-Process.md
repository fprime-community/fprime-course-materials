This file seeks to give a quick reference for the development process used for the FSW workshop.

# Ports

In order to add new ports into the system follow the following steps.

**Note:** adding files below is easiest by copying from an existing port and editing it.

1. Create a new port directory 
2. Add `mod.mk` and `Makefile` to that directory
3. Add port directory to `mk/configs/modules/modules.mk`
4. Create a port `*Ai.xml` file and fill it out
5. Add the `*Ai.xml` to `mod.mk` in port directory
6. In the port directory: `make gen_make`
7. In the port directory: `make` to autocode the port

# Components

**Note:** adding files below is easiest by copying from an existing component and editing it.

1. Create a new component directory 
2. Add `mod.mk` and `Makefile` to that directory
3. Add the component directory to `mk/configs/modules/modules.mk`
4. Create a component `*Ai.xml` file and fill it out
6. Add `*Ai.xml` to `mod.mk` in component directory
7. In the component directory: `make gen_make`
8. In the component directory: `make` to autocode the port
9. Generate implementations using `make impl` in component directory
10. Rename the generated `*-template` files to remove the `-template` suffix
11. Add new `*Impl.cpp` and `*Impl.hpp` files to `mod.mk` in component directory
12. `make gen_make` in component directory
13. `make` in component directory
