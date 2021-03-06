[ ![Download](https://api.bintray.com/packages/bincrafters/public-conan/glfw%3Abincrafters/images/download.svg) ](https://bintray.com/bincrafters/public-conan/glfw%3Abincrafters/_latestVersion)
[![Build Status](https://travis-ci.org/bincrafters/conan-glfw.svg?branch=stable%2F3.2.1)](https://travis-ci.org/bincrafters/conan-glfw)
[![Build status](https://ci.appveyor.com/api/projects/status/8d1mon7v51qa2jaw?svg=true)](https://ci.appveyor.com/project/BinCrafters/conan-glfw)

[Conan.io](https://conan.io) package for [glfw](https://github.com/glfw/glfw) project

The packages generated with this **conanfile** can be found in [Bintray](https://bintray.com/bincrafters/public-conan/glfw%3Abincrafters).

## For Users: Use this package

### Basic setup

    $ conan install glfw/3.2.1@bincrafters/stable

### Project setup

If you handle multiple dependencies in your project is better to add a *conanfile.txt*

    [requires]
    glfw/3.2.1@bincrafters/stable

    [generators]
    cmake

Complete the installation of requirements for your project running:

    $ mkdir build && cd build && conan install ..

Note: It is recommended that you run conan install from a build directory and not the root of the project directory.  This is because conan generates *conanbuildinfo* files specific to a single build configuration which by default comes from an autodetected default profile located in ~/.conan/profiles/default .  If you pass different build configuration options to conan install, it will generate different *conanbuildinfo* files.  Thus, they should not be added to the root of the project, nor committed to git.

If you are going to be using the Vulkan API, you have to have a Vulkan SDK installed, e.g. by setting up the [LunarG Vulkan SDK](https://www.lunarg.com/vulkan-sdk/). You also need to make sure that conan compiles glfw locally so that Vulkan can be detected, which would mean that `conan install` has to be executed with the `--build glfw` flag in the abovementioned commands:

    $ mkdir build && cd build && conan install .. --build glfw
	
If you are using CMake, you still have to call `find_package(Vulkan REQUIRED)`, include the `${Vulkan_INCLUDE_DIR}` directory and link to `${Vulkan_LIBRARY}` in your CMakeLists. 
	
Specifically when using the LunarG Vulkan SDK on Windows, if the build procedure cannot detect Vulkan or if there are linking errors, just do the following:

**For 32-bit builds:** Copy all the .lib files from the Vulkan SDK `Lib32` directory to the Vulkan SDK `Bin32` directory.

**For 64-bit builds:** Copy all the .lib files from the Vulkan SDK `Lib` directory to the Vulkan SDK `Bin` directory. Rename the Vulkan SDK `Bin32` directory to `Bin32_` and the `Bin` directory to `Bin32`. 

This is an ugly hack but it is needed to accommodate the FindVulkan cmake module that comes with glfw v3.2.1, which is not perfect. This problem has been corrected in the glfw trunk and it won't be an issue when the next version gets released.

## For Packagers: Publish this Package

The example below shows the commands used to publish to bincrafters conan repository. To publish to your own conan respository (for example, after forking this git repository), you will need to change the commands below accordingly.

## Build and package

The following command both runs all the steps of the conan file, and publishes the package to the local system cache.  This includes downloading dependencies from "build_requires" and "requires" , and then running the build() method.

    $ conan create bincrafters/stable

## Add Remote

    $ conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"

## Upload

    $ conan upload glfw/3.2.1@bincrafters/stable --all -r bincrafters

## License
[ZLIB](https://github.com/glfw/glfw/blob/master/LICENSE.md)
