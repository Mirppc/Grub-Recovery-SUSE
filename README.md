# Grub-Recovery-SUSE
A helpful guide on how to recover from a broken grub install and also how to repair your suse system with access to the system's yast utility.

Original article from caf4926 on the Opensuse forums.  This guide will teach you how to rescue your grub on SLE 12, Leap and Tumbleweed as well as get access to YAST to fix any broken runlevels and other modifications.  

Boot the Rescue from the DVD or the RescueCD. This should be the same Arch as the installation: ie; 32 bit or 64 bit...
Also includes the steps to get YAST working by mounting sys and proc before chroot.

# Grub Recovery

Once the DVD rescue gets to 'login', type: root
from there I run fdisk -l to confirm my HD partitition order.

My root partition is /dev/sda3 in this guide and is where /boot is.

See below for more instuctions for a seperate /boot partition

We need to mount root (for me that's sda3)

Now mount / (sda3) with

> mount /dev/sda3 /mnt

To mount the other devices next do

>mount --bind /dev /mnt/dev

>mount --bind /proc /mnt/proc

>mount --bind /sys /mnt/sys

Then chroot

>chroot /mnt

Your prompt changes to: Rescue:/>

Here type: 

>mkinitrd

Then do

>grub2-mkconfig -o /boot/grub2/grub.cfg

>grub2-install /dev/sda

Then to reboot you type exit and then reboot as follows.

>exit

>reboot

This also allows one to have access to YAST hence the binding of sys and proc before chroot.

If you use LVM please check this post: https://forums.opensuse.org/vbcms-comments/478290-article-re-install-grub2-dvd-rescue-3.html#post2519005

You can see it all here: https://dl.dropbox.com/u/10573557/Gr...ect/rescue.jpg

N.B: This method should also work from a DVD or the RescueCD and doesnt matter if version type is different.  You can use a Opensuse Leap disc to rescue a SLES install and vice versa.

The discs should be the same Architecture as the installation: ie; 32 bit or 64 bit..USE DVD OR RESCUE CD

# Seperate /boot partition instructions

If you have a seperate /boot partition you will also need to mount that before you chroot.
in this example /boot will be in /dev/sda2

>mount /dev/sda2 /mnt/boot

Continue as above with the mounting of /dev to /mnt/dev.


Sources: 
caf4926. “Re-Install Grub2 from DVD Rescue.” OpenSUSE Forums RSS, OpenSUSE, 12 Sept. 2012, forums.opensuse.org/content.php/128-Re-install-Grub2-from-DVD-Rescue.

If you liked this please help me buy a cup of tea or some food via Librepay.


<noscript><a href="https://liberapay.com/Mir/donate"><img alt="Donate using Liberapay" src="https://liberapay.com/assets/widgets/donate.svg"></a></noscript>
