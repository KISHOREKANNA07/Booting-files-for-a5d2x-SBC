# SD Card Flashing in Rugged Board

![Rugged Board](your-image-path/ruggedboard.jpg)

This guide provides steps to fix NOR flash issues using the SD card flashing method on the Rugged Board A5d2x.

## Overview

NOR flash may become unsupported or corrupted. The solution is to flash the image file using an SD card.

## Requirements

### Hardware:
- SD Card Reader/Writer for PC
- SD Card
- Rugged Board A5d2x

### Software:
- GParted
- Ubuntu 16.04
- minicom

### Required Files:
Use your own binary images or download from the provided link. The necessary files include:
- `BOOT.BIN`
- `u-boot.bin`
- `a5d2x-rugged_board.dtb`
- `zImage`
- `rb-sd-core-image-minimal-rugged-board-a5d2x.tar.gz`

## Procedure

### 1. Preparing the Bootable SD Card

1. Insert the SD Card into your PC.
2. Open **GParted** (password required).
3. Select the SD Card device from the top-right corner.

   ![GParted Selection](your-image-path/gparted-selection.png)

4. Unmount and delete all existing partitions.
5. Create a new partition:
   - **Type:** `fat32`
   - **Size:** `2048 MB`
   - **Label:** `boot`
6. Create a second partition:
   - **Type:** `ext3`
   - **Size:** `1024 MB`
   - **Label:** `rootfs`

   ![Partition Creation](your-image-path/partition-creation.png)

7. Apply the changes and set the **boot flag** on the boot partition.

   ![Set Boot Flag](your-image-path/boot-flag.png)

### 2. Copying Files to the SD Card

1. Copy the following files to the **boot** partition:
   ```sh
   cp BOOT.BIN u-boot.bin a5d2x-rugged_board.dtb zImage /mnt/boot/
   ```
2. Extract the root filesystem tar file to the **rootfs** partition:
   ```sh
   tar -xvzf rb-sd-core-image-minimal-rugged-board-a5d2x.tar.gz -C /mnt/rootfs/
   ```

### 3. Booting the Board with SD Card

1. Insert the SD card into the Rugged Board A5d2x.
2. Connect the board to your PC via USB.
3. Open **minicom**.
4. Press the **RESET** button to boot.

   ![Booting the Board](your-image-path/booting-board.jpg)

5. Log in with:
   ```sh
   Username: root
   ```
6. If a warning occurs, check if the board switch is set to **boot mode**.
7. Press **RESET** again; the image file will start flashing.

## Troubleshooting

- If the board does not boot, ensure the boot switch is correctly set.
- If errors persist, reformat the SD card and repeat the steps.

For more details, visit [RuggedBoard Documentation](https://ruggedboard.com/).
