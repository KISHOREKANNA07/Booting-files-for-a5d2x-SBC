# Fixing Error of NOR Flash Using SD Card Flashing in Rugged Board

This guide provides steps to fix NOR flash issues using the SD card flashing method on the Rugged Board A5d2x.

## Overview

NOR flash may become unsupported or corrupted. The solution is to flash the image file using an SD card.

## Requirements

### Hardware:
- SD Card Reader/Writer for PC
- SD Card
- Rugged Board A5d2x

![Rugged Board A5d2x](https://your-image-link.com/rugged-board.jpg)

### Software:
- GParted
- Ubuntu 20.04
- minicom

### Required Files:
Use your own binary images or download from the provided link. The necessary files include:
- `BOOT.BIN`
- `u-boot.bin`
- `a5d2x-rugged_board.dtb`
- `zImage`
- `rb-sd-core-image-minimal-rugged-board-a5d2x.tar.gz`

## Procedure

  ![Connection Diagram]()
  
### 1. Preparing the Bootable SD Card

1. Insert the SD Card into your PC.
2. Open **GParted** (password required).
3. Select the SD Card device from the top-right corner.

   ![GParted SD Card Selection]()

4. Unmount and delete all existing partitions.
5. Create a new partition:
   - **Type:** `fat32`
   - **Size:** `2048 MB`
   - **Label:** `boot`

   ![Create Boot Partition](https://your-image-link.com/create-boot-partition.jpg)

6. Create a second partition:
   - **Type:** `ext3`
   - **Size:** `1024 MB`
   - **Label:** `rootfs`

   ![Create RootFS Partition](https://your-image-link.com/create-rootfs-partition.jpg)

7. Apply the changes and set the **boot flag** on the boot partition.

### 2. Copying Files to the SD Card

1. Copy the following files to the **boot** partition:
   ```sh
   cp BOOT.BIN u-boot.bin a5d2x-rugged_board.dtb zImage /mnt/boot/
