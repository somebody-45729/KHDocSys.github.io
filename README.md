theme: jekyll-theme-minimal
description: Kyunghoon Han CS-3353-01 Arch Installation Documentation

# Note I put commands
1. Download Arch from a preferred medium [I did through USB]. Other mediums are avilable through wiki.archlinux.org/title/Installation_guide

2. Make sure, when using VMWare Workstation to access the directory to boot it into UEFI mode by inserting code firmware = efi into line 2 of .vmx file

3. Now we must create sda(s) by entering code [fdisk -l] or [cfdisk /dev/sda] to begin the parition process # Selected GPT for later use for GRUB

4. Once you are able to access the free space needed to create the partitions, create sda1 (512 MB) and sda2 (The rest)

# Note, be sure to make the partitions 100% correct for your needed procedures. I completely messed up mine twice (I had sda1 - sda4 with unnecessary additions)

# Again, make sure whatever partitions you create, that they are correct types and storage

5. Format sda1 as [mkfs.fat -F32 /dev/sda1] and sda2 (the root) as [mkfs.ext4 /dev/sda2] # The necessary formats for each sda

6. Mount sda2 (root partition) as [mount /dev/sda2 /mnt]. Then create a directory using [mkdir /mnt/boot] and mount the EFI (sda1) to it using [mount /dev/sda1 /mnt/boot]

7. Now we must generate an fstab file so when the system boots it knows where to mount the partitions. [genfstab -U /mnt >> /mnt/etc/fstab] is the command.

8. Chroot the system using [arch-chroot /mnt] and  input the command [ln -sf /usr/share/zoneinfo/US/Central /etc/localtime] for the sake of localization of the machine

9. Localization may require you to install nano through pacman -S, so once that is done, use the command [nano /etc/locale.gen] to edit/uncomment needed locales, specifically en_US.ETF-8 UTF-8.

10. I choose NetworkManager using [pacman -S networkmanager] and enabled it by [systemctl enable NetworkManager.service]. Also check and see with type of microcode is needed.

# Microcode depends on aspect of whether or not it is Intel or AMD based
11. We will be installing the grub bootloader; Installed using [grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB];

# You may or may not need to install necessary packages before this
12. After grub bootloader is installed, we now just need the configuration file. The following command [grub-mkconfig -o /boot/grub/grub.cfg] to do so.

13. Now exit out of the chroot, manually unmount all partitions using [umount -R /mnt] and then reboot. (This is the part where you can now install a DE like Gnome).

14. From this point, we will be installing the DE GNOME. But before that, we must now install X Window System (Xorg) with the command [pacman -S xorg xorg-server].

15. Then install the Desktop Environment using [pacman -S gnome]; Also command in [pacman gnome-extra gdm] as well to cover the bases overall.

16. Once you have used the pacman command for everything necessary for GNOME, use the command [(sudo) systemctl enable gdm]. 

# The DE will now appear everytime after system boot
# That should cover everything in regards to the installation guide before moving forward with the GUI

https://utulsa.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=df525820-bec7-4efd-8a80-add10013e761&start=0 (panopto walkthrough video)
