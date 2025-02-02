# SD Card Flashing in Rugged Board

## Overview

This is solution to flash the image file in rugged board a5d2x using an SD card.

## Requirements

### Hardware:
- SD Card Reader/Writer for PC
- SD Card
- Rugged Board A5d2x

### Software:
- GParted
- Ubuntu 20.04
- minicom

### Required Files:
Use your own binary images or download from the repository. The necessary files include:
- `BOOT.BIN`
- `u-boot.bin`
- `a5d2x-rugged_board.dtb`
- `zImage`
- `rb-sd-core-image-minimal-rugged-board-a5d2x.tar.gz`

## Procedure

### 1. Preparing the Bootable SD Card

1. Insert the SD Card into your PC.
   
    ![Connection Diagram](https://github.com/user-attachments/assets/7dd37cef-6f24-47d7-9fe3-8bf6b94c4d00)
   
3. Open **GParted** (password required).

   ![GParted Selection](https://github.com/user-attachments/assets/8ad335db-858e-4e6c-89f8-e619fbdfd7cd)
   
4. Select the SD Card device from the top-right corner.

   ![Select SD card](https://github.com/user-attachments/assets/46442307-1c65-4016-bfa5-083d485c59b1)

6. Unmount and delete all existing partitions.

   ![Unmounted Partition](https://github.com/user-attachments/assets/629262fb-7c59-47f3-905f-910c08273e67)
   
8. Create a new partition:
   - **Type:** `fat32`
   - **Size:** `2048 MB`
   - **Label:** `boot`
9. Create a second partition:
   - **Type:** `ext3`
   - **Size:** `1024 MB`
   - **Label:** `rootfs`

   ![Unmounted Partition](https://github.com/user-attachments/assets/5e924e89-ff37-4efc-8773-e162df5792f6)
   ![Click ok](https://github.com/user-attachments/assets/934bf6c7-d5b4-433d-9a02-751e2b111a97)
10. Apply the changes and set the **boot flag** on the boot partition.

      ![Set Boot Flag](https://github.com/user-attachments/assets/5535ad03-0932-4b11-be08-0319f17f1236)

### 2. Copying Files to the SD Card

1. Copy the below images to boot partition
   
   - **BOOT.BIN**
   - **u-boot.bin**
   - **a5d2x-rugged_board.dtb** 
   - **zImage**

2. And the root file system tar file should be extracted to the rootfs partition of the SD Card using the below commands.
   ```sh
   sudo tar -xvf <path of the rootfs tar file> -C <path to copy on rootfs partition>
   ```

3. Extract the root filesystem tar file to the **rootfs** partition:
   ```sh
   sudo tar -xvzf rb-sd-core-image-minimal-rugged-board-a5d2x.tar.gz -C /media/hostname/rootfs/
   ```

### 3. Booting the Board with SD Card

1. Insert the SD card into the Rugged Board A5d2x.
2. Connect the board to your PC via USB.
3. Open **minicom**.
    ```sh
   sudo minicom
   ```
5. Press the **RESET** button to boot.
6. Log in with:
   ```sh
   Username: root
   ```
7. If a warning occurs, check if the board switch is set to **boot mode**.
   
   ![Booting the Board](https://github.com/user-attachments/assets/c4c68a22-f126-4c50-8416-3ac4c8d97688)
   
10. Press **RESET** again; the image file will start flashing.

    ![Seccessful booting](https://github.com/user-attachments/assets/cfaae77d-fcb1-4bfc-a6ce-623953d24432)

## Troubleshooting

- If the board does not boot, ensure the boot switch is correctly set.
- If errors persist, reformat the SD card and repeat the steps.
