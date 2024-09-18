# apptainer_wrapper / singularity_wrapper

This small script helps with running apptainer / singularity images.

It is especially useful when using Lmod or other module system that can set environment variables.

## Usage

Set the `$PATH` to point to the `bin`-folder.

Afterwards, you can set these two environment variables:

- `$CONTAINER_IMAGE` - Path to the apptainer / singularity image that should be used.
- `$CONTAINER_FLAGS` - Extra flags that should be added to every apptainer / singularity call (e.g `-B /my_folder`, `--nv`).

After these have been set one can run:

- `apptainer_wrapper run` - same as running `apptainer run $CONTAINER_FLAGS $CONTAINER_IMAGE`
- `apptainer_wrapper exec my_executable` - same as running `apptainer exec $CONTAINER_FLAGS $CONTAINER_IMAGE my_executable`
- `apptainer_wrapper shell` - same as running `apptainer shell $CONTAINER_FLAGS $CONTAINER_IMAGE`
- `apptainer_wrapper shell /bin/bash` - same as running `apptainer shell -s /bin/bash $CONTAINER_FLAGS $CONTAINER_IMAGE`

## Example Lmod module

```lua
-- -*- lua -*-
--
-- Module file for singularity-wrapper
--

whatis([[Name : my-image]])
whatis([[Version : latest]])
help([[A software in ]])

family("container")

prepend_path("PATH", "/path/to/singularity_wrapper/bin")
setenv("CONTAINER_IMAGE", "/path/to/singularity/image/my-image-latest.sif")
setenv("CONTAINER_FLAGS", " -B /my_binding --nv ")
```
