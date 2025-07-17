This is just for learning purpose.
# KernelSU Action
This is created by https://github.com/xiaoleGun
and modifications introduced by https://github.com/bxySo
I hold no creative authority over this.(thanks to original developer)
pls checkout their original work.
**KernelSU Action** is an automation tool for building non-GKI (Non-Generic Kernel Image) kernels with **KernelSU** integration for Android devices. It uses **GitHub Actions** to streamline the process of compiling, customizing, and flashing your kernel with KernelSU support. This action is intended for developers familiar with kernel building and Android.

> **Warning**: If you are using someone else’s kernel, please use this action for personal use only. Do not redistribute others' work. Respect the author's intellectual property.

---

## Supported Kernel Versions
- **5.4**
- **4.19**
- **4.14**
- **4.9**

---

## Features

- **Kernel Customization**: 
  - Supports custom kernel sources, branches, and configurations.
  - Modify kernel parameters like kprobes and overlayfs to enable **KernelSU** support.
  
- **Compiler Support**: 
  - Use custom **Clang** (e.g., **Proton Clang**) or **GCC** compilers.
  - Select Clang versions corresponding to different Android releases (e.g., Android S, T, U).
  
- **KernelSU Integration**: 
  - Easily integrate **KernelSU** for systemless root on non-GKI kernels.
  - Option to specify a custom **KernelSU** repository and version.

- **AnyKernel3 Support**:
  - Customize and use **AnyKernel3** to package the kernel into a flashable boot image.
  
- **Build Speed Optimization**:
  - Enable **ccache** to speed up subsequent builds by caching previous build outputs.

- **DTBO Support**: 
  - Optionally build and upload a **Device Tree Blob (DTBO)** for devices that require it.

- **Post-Build Flashing**: 
  - The resulting build is packaged into a flashable `.zip` (using AnyKernel3), ready for TWRP or other recovery environments.

---

## Usage

### 1. Fork the Repository

Fork this repository to your GitHub account.

### 2. Configure `config.env`

Edit the `config.env` file in your fork with the following key variables:

- **KERNEL_SOURCE**: Your kernel repository URL (e.g., `https://github.com/yourusername/your_kernel_repo`).
- **KERNEL_BRANCH**: The branch of the kernel to use (e.g., `main`, `tda`).
- **KERNEL_CONFIG**: Path to the kernel config file (e.g., `vendor/your_defconfig`).
- **ARCH**: Architecture of your device (e.g., `arm64`).
- **KERNEL_IMAGE**: Name of the kernel image to flash (e.g., `Image.gz-dtb`).
- **CLANG_VERSION**: Version of Clang to use (e.g., `14.0.6` for Android T).
- **KERNELSU_TAG**: Tag or branch for **KernelSU** (e.g., `v0.9.5`).

Optional:
- Enable **ccache** to cache builds and speed up the process.
- Enable **DTBO** if your device requires a device tree blob.

Here’s an example configuration:

```env
KERNEL_SOURCE=https://github.com/yourusername/your_kernel_repo
KERNEL_BRANCH=main
KERNEL_CONFIG=vendor/your_defconfig
ARCH=arm64
KERNEL_IMAGE=Image.gz-dtb
CLANG_VERSION=14.0.6
KERNELSU_TAG=v0.9.5
ENABLE_KERNELSU=true
```

### 3. Start the Build

1. Navigate to the **Actions** tab in your forked repository.
2. Click on the **Build Kernel** option and select **Run workflows**.

### 4. Flash the Kernel

Once the build is successful, the **AnyKernel3** zip file will be uploaded. Download the zip and flash it via **TWRP** or your preferred recovery environment.

---

## KernelSU Integration

To integrate **KernelSU**, ensure that the `ENABLE_KERNELSU` variable is set to `true`. You can specify the version of **KernelSU** to use by setting the `KERNELSU_TAG` variable (e.g., `v0.9.5` for the latest stable release). If you need a custom **KernelSU** repository or version, specify the GitHub repository and branch/tag.

### KernelSU Manager Signature

If you need to customize the signature size or hash for **KernelSU**, set the following variables in your `config.env`:

```env
KSU_EXPECTED_SIZE=0x033b
KSU_EXPECTED_HASH=c371061b19d8c7d7d6133c6a9bafe198fa944e50c1b31c9d8daa8d7f1fc2d2d6
```

You can obtain the signature size and hash with the `ksud debug get-sign <apk_path>` command.

---

## Optional Build Customizations

- **Custom Clang**: You can use custom Clang toolchains (e.g., **Proton Clang**) by specifying the Git repository or zip file URL.
- **Enable GCC**: Support for GCC cross-compilers is available. You can enable **GCC 32** or **GCC 64** if required.
- **Extra Compilation Commands**: Some kernels require additional commands for correct compilation. Add any necessary flags to the `Extra cmds` section.
- **LTO Optimization**: Option to disable **LTO** if it causes errors during the build.

---

## Additional Information

### Kernel Source and Configuration

Make sure your kernel source and configuration are compatible with your device. You can set the kernel source as a GitHub repository link (e.g., `https://github.com/yourusername/your_kernel_repo`) and specify the branch and defconfig file for the build.

### AnyKernel3

This action uses **AnyKernel3** to package the compiled kernel into a bootable image. You can provide your own **AnyKernel3** repository or use the default one.

If you wish to use a custom **AnyKernel3**, specify the repository link in the `AnyKernel3 Source` field.

### DTBO

Some devices require a **Device Tree Blob (DTBO)**. If your device needs one, enable the **Need DTBO** option to have it included in the final image.

---

## Acknowledgements

- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [xiaoxindada](https://github.com/xiaoxindada)

---

This action simplifies the process of building custom kernels with **KernelSU** support. Whether you’re experimenting with kernel tweaks or creating custom Android builds, this tool streamlines the process of kernel compilation and flashing.

---

This refined README organizes the information, clarifies the steps, and provides clear explanations of each option to help users effectively configure and use the **KernelSU Action**.
