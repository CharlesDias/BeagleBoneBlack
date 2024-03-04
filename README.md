# BeagleBone Black

## Bitbake commands

* Show some command options.
```
$ bitbake -h
```

* Build image.

```
$ bitbake <image-name>
```

* Build image and continue as much as possible after an error.
```
$ bitbake -k <image-name>
```

* Show layers
```
$ bitbake-layers show-layers
```

* List of the available image recipes inside of Poky folder.
```
$ ls poky/meta*/recipes*/images/*.bb
```

* List of the available machine supported.
```
$ ls poky/meta*/conf/machine/*.conf
```

* Check the variable value

```console
$ bitbake -e <image-name> | grep ^<variable-name>
```

Example

```console
$ bitbake -e core-image-minimal | grep ^IMAGE_INSTALL
```

* To help you see where you currently are with kernel and root filesystem sizes, you can use two tools found in the Source Directory in the scripts/tiny/ directory:

ksize.py: Reports component sizes for the kernel build objects.

dirsize.py: Reports component sizes for the root filesystem.

* Clean a recipe

```console
bitbake recipe-name -c cleansstate
```

or 

```console
bitbake recipe-name -c cleanall
```

For example, to clean the current kernel recipe and rebuild the image:

```console
bitbake -c cleanall virtual/kernel
bitbake your-image-name
```

In Yocto Project, `cleansstate` and `cleanall` are two different tasks that you can run with the `bitbake -c` command. They both clean the output files for a recipe, but they do it in slightly different ways:

- `cleanall`: This task removes all output files for a recipe. This includes the files in the `WORKDIR` directory, the shared state cache (sstate) files, and the deploy files. After running `cleanall`, you can rebuild the recipe from scratch with `bitbake`.

- `cleansstate`: This task is similar to `cleanall`, but it does not remove the deploy files. The deploy files are the final output files of a recipe, such as images, packages, and SDKs. After running `cleansstate`, you can rebuild the recipe from scratch with `bitbake`, but the old deploy files will still be available.

In general, you should use `cleansstate` if you want to rebuild a recipe but keep the old deploy files, and `cleanall` if you want to completely remove all output files for a recipe.

* Open the menuconfig

```console
bitbake -c menuconfig virtual/kernel
```

# - run the command "ps ax" inside the bbb and check if the /sbin/init is the first process
# - type the sys and press tab. Check on output console the commands starting by sys*
# - check on dmesg the messages started by systemd
