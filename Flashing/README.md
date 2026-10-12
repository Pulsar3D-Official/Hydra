#Firmware Flashing

##CAN with Katapult

First of all, make sure CAN is already set up on your printer. You can follow Esoterical's guide here: [https://canbus.esoterical.online/](https://canbus.esoterical.online/)
    1. Connect the Hydra to USB on your Pi.
    2. SSH into Pi.
    3. Install Katapult using ```git clone https://github.com/Arksine/katapult```
    4. Go to ~/klipper, do a make clean, then make menuconfig, use the Klipper settings below, then make.
    5. Go to the Katapult directory cd ~/katapult/, do a make clean, then make menuconfig, use the Katapult settings below, then make.
    6. On the Hydra, hold the BOOT button. While holding it press and release the RESET button, then release the BOOT button.
    7. Use lsusb to verify that your Hydra is in DFU mode.
    8. Flash Katapult using ```sudo dfu-util -R -a 0 -s 0x08000000:mass-erase:force:leave -D ~/katapult/out/katapult.bin -d 0483:df11```.
    9. Use ```~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0``` to find Hydra's UUID. It'll say Canboot next to it.
    10. Flash Klipper using  ```cd ~/katapult/scripts && python3 flashtool.py -i can0 -f ~/klipper/out/klipper.bin -u <uuid>```, replace <uuid> with your Hydra's UUID.

##USB with Katapult

    1. Connect the Hydra to USB on your Pi.
    2. SSH into Pi.
    3. Install Katapult using ```git clone https://github.com/Arksine/katapult```
    4. Go to ~/klipper, do a make clean, then make menuconfig, use the Klipper settings below, then make.
    5. Go to the Katapult directory ```cd ~/katapult/```, do a make clean, then make menuconfig, use the Katapult settings below, then make.
    6. On the Hydra, hold the BOOT button. While holding it press and release the RESET button, then release the BOOT button.
    7. Use lsusb to verify that your Hydra is in DFU mode.
    8. Flash Katapult using sudo ```sudo dfu-util -R -a 0 -s 0x08000000:mass-erase:force:leave -D ~/katapult/out/katapult.bin -d 0483:df11```.
    9. Use ```ls /dev/serial/by-id``` to find Hydra's Serial ID. It'll say Katapult in the ID.
    10. Go to the Klipper directory ```cd ~/klipper```.
    11. Flash Klipper using  ```make flash FLASH_DEVICE=/dev/serial/by-id/usb-katapult_your_board_id```, replace your_board_id with your Hydra's serial ID.

##USB without Katapult

    1. cd ~/klipper
    2. make clean
    3. make menuconfig, use the Klipper settings below
    4. make flash FLASH_DEVICE=0483:df11
