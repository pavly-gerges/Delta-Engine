# Delta-Engine

A realtime Newtonian-based physics and hardware engine library with an API designed to address problems of simulation and real object dynamics; the idea is to couple building a physics simulator with emulating IO using the same abstraction via polymorphism and encapsulation (e.g., building a human joint simulator on a 3D game engine and deploying it on a hardware stepper motor module to emulate the same motion using electronic components in a different system using the same code).

## General List of supported features
- [ ] N-dimensional Physics Spaces.
- [ ] CPU-based Realtime monitoring.
- [ ] Support for Classical Linear Newtonian Mechanics.
- [ ] Support for Classical Rotational Newtonian Mechanics.
- [ ] Operates its pipeline using Newton's Laws of Motion.
- [ ] Uses pure vectorial structures from the _Electrostatic SDK_.
- [ ] Wires the software simulation with your hardware abstraction layer that controls the outside environment based on the provided physical model.

## Problems and solutions preview
| Problems | Solutions |
|----------|-----------|
| N-dimensionality: | | 
| Creating physics spaces: | |
| Motion-based runtime environment: | |
| Attaching and detaching objects with physical properties: | |
| Equilibrium and forces: | |
| Transforming objects using external linear momentums: | |
| Transforming objects using external linear forces: | |
| Transforming objects using external angular momentums: | |
| Transforming objects using external angular forces: | |
| Transforming objects using other objects in space (Newton's third law): | |
| Collision detection of objects in the physics space: | |
| Collision avoiding objects in the physics space: | | 
| Updating objects in realtime based on CPU slices: | |
| Physical objects groups and group physics: | |

## Setup the Electrostatic Environment
This will install missing dependencies (CLI tools and toolchains) in `/opt/electrostatic-sandbox` that shall be utilized by the SDK build front-end and CMake to build the applications.

```bash
chmod +rwx ./helper-scripts/setup-environment/setup-sandbox.sh && \
           ./helper-scripts/setup-environment/setup-sandbox.sh
```
> [!IMPORTANT]
> Windows devices will require Windows-Subsystem for Linux (WSL) and a distribution package to be installed; make sure to setup them on your machine via the powershell:
> 1) Run a new powershell or a windows terminal powershell session as administrator.
> 2) Set the execution policy of the current session for the current process as "Bypass" to enable running unauthorized scripts, which will be reverted normally to the default "restricted" policy when this session is over: 
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
> ```
> 3) Run the script:
> ```powershell
> setup-wsl-debian.ps1
> ```
> 4) Reboot if needed, and follow-on to enable BIOS/UEFI CPU virtualization if necessary.
> 5) The script enables the WSL and windows virtualization features, download WSL Debian Distribution binaries, and sets up the `usbipd` utility for routing usb ports across servers.
> 6) Continue with setting up and customizing your development environment.

## Build the application binary (.elf)
This will build the application binary to all supported platforms; usually if a new build routine is to be built, it has to go here.

```bash
chmod +x ./helper-scripts/project-impl/compile-all.sh && \
         ./helper-scripts/project-impl/compile-all.sh 
```

## Introducing other building routines using Bash
Introducing other building routines is far easy. However, it's mostly dependent on whether the original SDK is supporting those platforms. If not yet, you will have to build a pre-compilation header that excludes the SDK for those unsupported systems or else you will get linking errors.

Usually the build routines will look like that in general:
https://github.com/Electrostat-Lab/Electrostatic-Library/blob/a6d9669dde096c02285e28c5657aa2438793b367/helper-scripts/project-impl/compile-all-linux.sh#L1-L17

They are dependent on that abstraction: 
https://github.com/Electrostat-Lab/Electrostatic-Library/blob/a6d9669dde096c02285e28c5657aa2438793b367/helper-scripts/abstract/abstract-compile.sh#L1-L41

## Adding new examples to test the introduced APIs
* Adding new examples could be achieved by creating new source code (single source files) under the `examples` module, and using the following command to compile and run the example:
```bash
$ ./helper-scripts/project-impl/compile-examples.sh "-m64" "main.cpp" "executable-example" "linux" "x86-64" "x86-64/exe"
$ ./cmake-build/linux/x86-64/exe/executable-example.elf
```
> [!NOTE]
> This command links the specified source example against the `Electrostatic-Sandbox SDK` libraries and the `Electroextension` library (your native library).

* Adding new examples for microcontroller programming is much the same, but will require uploading as a post-compilation script.
