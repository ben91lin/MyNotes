    sudo -i
    apt-cache search linux-image-*\.*\.**-generic
    apt-cache search linux-modules-extra-*\.*\.**-generic
    apt install linux-image-*\.*\.**-generic
    apt install linux-modules-extra-*\.*\.**-generic
    update-initramfs -u -k all
    update-grub
    reboot