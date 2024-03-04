# BeagleBone Black

## Bitbake commands

List of general BitBake commands:

| Command | Description |
| --- | --- |
| `bitbake -h` | Show some command options. |
| `bitbake <image-name>` | Build the image-name, per example, `bitbake core-image-minimal`. |
| `bitbake -k <image-name>` | Build the image-name and continue as much as possible after an error. |
| `bitbake -e <image-name> \| grep ^<variable-name>` | Check the variable value from a image-name. for example, `bitbake -e core-image-minimal \| grep ^IMAGE_INSTALL` |
| `bitbake-layers show-layers` | Shows the currently configured layers. |
| `bitbake-layers add-layer <layer>` | Adds a layer to the configuration. |
| `bitbake-layers remove-layer <layer>` | Removes a layer from the configuration. |
| `bitbake-layers show-recipes` | Shows the recipes provided by the currently configured layers. |
| `bitbake <recipe>` | Builds a recipe. |
| `bitbake -c <task> <recipe>` | Runs a specific task for a recipe. |
| `bitbake -k <recipe>` or `bitbake -k` | Continues as much as possible after an error. |
| `bitbake -v <recipe>` | Gives verbose output. |
| `bitbake -e <recipe>` | Shows the environment variables for a recipe. |
| `bitbake -c clean <recipe>` | Removes all output files for a recipe. |
| `bitbake -c cleansstate <recipe>` | Removes all output files and shared state cache for a recipe. |
| `bitbake -c cleanall <recipe>` | Removes all output files, shared state cache, and downloaded source files for a recipe. |
| `bitbake -c devshell <recipe>` | Opens a shell with the environment set up for development/debugging of the recipe. |
| `bitbake -c fetch <recipe>` | Fetches the source files for a recipe. |
| `bitbake -c compile <recipe>` | Compiles the source files for a recipe. |
| `bitbake -c package <recipe>` | Creates packages from the compiled files for a recipe. |
| `bitbake -c deploy <recipe>` | Deploys the packages for a recipe. |

Remember to replace `<recipe>` and `<task>` with the actual recipe name and task name respectively. For example, to work through `virtual/kernel`, we can use the some commands as shown below:

| Command | Description |
| --- | --- |
| `bitbake virtual/kernel` | Builds the kernel. |
| `bitbake -c compile virtual/kernel` | Compiles the kernel source code. |
| `bitbake -c clean virtual/kernel` | Removes all output files for the kernel. |
| `bitbake -c cleansstate virtual/kernel` | Removes all output files and shared state cache for the kernel. |
| `bitbake -c cleanall virtual/kernel` | Removes all output files, shared state cache, and downloaded source files for the kernel. |
| `bitbake -c devshell virtual/kernel` | Opens a shell with the environment set up for development/debugging of the kernel. |
| `bitbake -c menuconfig virtual/kernel` | Opens the kernel configuration menu (menuconfig). |
| `bitbake -c savedefconfig virtual/kernel` | Saves the current kernel configuration to the defconfig file. |
| `bitbake -c diffconfig virtual/kernel` | Shows the differences between the old and new kernel configuration. |
| `bitbake -c fetch virtual/kernel` | Fetches the kernel source files. |
| `bitbake -c deploy virtual/kernel` | Deploys the kernel image and modules. |
| `bitbake -c package virtual/kernel` | Creates packages from the compiled kernel files. |

## Other tips

 - [1. List of the available image recipes inside of Poky folder.](#1-list-of-the-available-image-recipes-inside-of-poky-folder)
 - [2. List of the available machine supported.](#2-list-of-the-available-machine-supported)
 - [3. Current kernel and root filesystem sizes](#3-current-kernel-and-root-filesystem-sizes)
 - [4. cleansstate and cleanall commands](#4-cleansstate-and-cleanall-commands)

### 1. List of the available image recipes inside of Poky folder.

```
ls poky/meta*/recipes*/images/*.bb
```

### 2. List of the available machine supported.

```
ls poky/meta*/conf/machine/*.conf
```

### 3. Current kernel and root filesystem sizes

To help you see where you currently are with kernel and root filesystem sizes, you can use two tools found in the Source Directory in the scripts/tiny/ directory:

 - ksize.py: Reports component sizes for the kernel build objects.

 - dirsize.py: Reports component sizes for the root filesystem.

### 4. cleansstate and cleanall commands

In Yocto Project, `cleansstate` and `cleanall` are two different tasks that you can run with the `bitbake -c` command. They both clean the output files for a recipe, but they do it in slightly different ways:

 - `cleanall`: This task removes all output files for a recipe. This includes the files in the `WORKDIR` directory, the shared state cache (sstate) files, and the deploy files. After running `cleanall`, you can rebuild the recipe from scratch with `bitbake`.

 - `cleansstate`: This task is similar to `cleanall`, but it does not remove the deploy files. The deploy files are the final output files of a recipe, such as images, packages, and SDKs. After running `cleansstate`, you can rebuild the recipe from scratch with `bitbake`, but the old deploy files will still be available.

In general, you should use `cleansstate` if you want to rebuild a recipe but keep the old deploy files, and `cleanall` if you want to completely remove all output files for a recipe.

### 