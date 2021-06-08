### FinalProject1
how to add your system call the Linux OS kernel.



Description of CPU:
![cpu](https://user-images.githubusercontent.com/85532323/121232734-3383fb00-c892-11eb-98da-575487053ec0.jpg)


Description of RAM:
![RAM](https://user-images.githubusercontent.com/85532323/121232913-5a423180-c892-11eb-9fdf-953182b2c747.jpg)



Description of kernal version:
![kernal](https://user-images.githubusercontent.com/85532323/121233042-81006800-c892-11eb-8353-528db4d77c0d.jpg)


Steps of how adding the system call:

1.Fully update your operating system:
sudo apt update && sudo apt upgrade -y


2.Download and install the essential packages to compile kernels
sudo apt install build-essential libncurses-dev libssl-dev libelf-dev bison flex -y
![1](https://user-images.githubusercontent.com/85532323/121233519-ff5d0a00-c892-11eb-9167-bc5cdde6ad8d.jpg)

 3.Clean up your installed packages:
 sudo apt clean && sudo apt autoremove -y
 ![2](https://user-images.githubusercontent.com/85532323/121233668-24517d00-c893-11eb-9092-2199f6836197.jpg)

4.Download the source code of the latest stable version of the Linux kernel (which is 5.12.9 as of 12) to your home folder:
wget -P ~/ https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.12.9.tar.xz
![3](https://user-images.githubusercontent.com/85532323/121233854-5d89ed00-c893-11eb-9a68-1e74ea815798.jpg)



5.Unpack the tarball you just downloaded to your home folder:
tar -xvf ~/linux-5.12.9.tar.xz -C ~/
![4](https://user-images.githubusercontent.com/85532323/121233974-814d3300-c893-11eb-8ef5-bf5fccf37a7f.jpg)


6.Reboot your computer



7.Check the version of your current kernel:
uname -r
![kernal](https://user-images.githubusercontent.com/85532323/121234518-151eff00-c894-11eb-9c8a-03194a8da752.jpg)



8.Change your working directory to the root directory of the recently unpacked source code:
cd ~/linux-5.12.9/
![5](https://user-images.githubusercontent.com/85532323/121234616-34b62780-c894-11eb-8207-43bf2f8738e8.jpg)


9. Create the home directory of your system call.

Decide a name for your system call, and keep it consistent from this point onwards. I have chosen identity.
mkdir identity
![6 1](https://user-images.githubusercontent.com/85532323/121234829-6d560100-c894-11eb-8489-8fcd5b12d665.jpg)

10.Create a C file for your system call.

Create the C file with the following command.
nano identity/identity.c
![6](https://user-images.githubusercontent.com/85532323/121234867-79da5980-c894-11eb-8429-1546617caed6.jpg)

Write the following code in it.
#include <linux/kernel.h>
#include <linux/syscalls.h>

SYSCALL_DEFINE0(identity)

{
    printk("I am Jihan Jasper Al-rashid.\n");
    return 0;
}


11.Create a Makefile for your system call.

Create the Makefile with the following command:
nano identity/Makefile
Write the following code in it.
obj-y := identity.o

![7](https://user-images.githubusercontent.com/85532323/121234982-a0989000-c894-11eb-89c1-33aa28bfe7de.jpg)


12.Add the home directory of your system call to the main Makefile of the kernel.

Open the Makefile with the following command.
nano Makefile
Search for core-y. In the second result, you will see a series of directories.

kernel/ certs/ mm/ fs/ ipc/ security/ crypto/ block/

In the fresh source code of Linux 5.8.1 kernel, it should be in line 1073.

Add the home directory of your system call at the end like the following.
kernel/ certs/ mm/ fs/ ipc/ security/ crypto/ block/ identity/
Save it and exit the editor.

13.Add a corresponding function prototype for your system call to the header file of system calls.

Open the header file with the following command.
nano include/linux/syscalls.h
Navigate to the bottom of it and write the following code just above #endif.
asmlinkage long sys_identity(void);
Save it and exit the editor.



14. Add your system call to the kernel's system call table.

Open the table with the following command.
nano arch/x86/entry/syscalls/syscall_64.tbl
Navigate to the bottom of it. You will find a series of x32 system calls. Scroll to the section above it. This is the section of your interest. Add the following code at the end of this section respecting the chronology of the row as well as the format of the column. Use Tab for space.
440     common  identity                sys_identity

![9](https://user-images.githubusercontent.com/85532323/121235430-2c122100-c895-11eb-99d4-32dca23789d6.jpg)

15.Configure the kernel.

Make sure the window of your terminal is maximized.

Open the configuration window with the following command.
make menuconfig
Use Tab to move between options. Make no changes to keep it in default settings.

Save and exit.

![10](https://user-images.githubusercontent.com/85532323/121235524-43e9a500-c895-11eb-8ac4-aa4836f16622.jpg)


16.Find out how many logical cores you have.

nproc

The following few commands require a long time to be executed. Parallel processing will greatly speed them up. For me, it is 6. Therefore, I will put 6 after -j in the following commands.

![11](https://user-images.githubusercontent.com/85532323/121235725-74c9da00-c895-11eb-9336-e3c7083f239b.jpg)

17.Compile the kernel's source code.
make -j6

![11](https://user-images.githubusercontent.com/85532323/121235936-ac388680-c895-11eb-970f-305e60863b66.jpg)

18. Prepare the installer of the kernel.
sudo make modules_install -j6

![13](https://user-images.githubusercontent.com/85532323/121236138-e9047d80-c895-11eb-8ee1-7e3e387f81da.jpg)

 19.Install the kernel.
sudo make install -j6
 - Update the bootloader of the operating system with the new kernel.
sudo update-grub
 - Reboot your computer.


20.Change your working directory to your home directory.
cd ~
4.3 - Create a C file to generate a report of the success or failure of your system call.

Create the C file with the following command.
nano report.c
Write the following code in it.

![14](https://user-images.githubusercontent.com/85532323/121237110-fc641880-c896-11eb-83fa-46e6115c8643.jpg)

21. Compile the C file you just created.
gcc -o report report.c
22. - Run the C file you just compiled.
./report
If it displays the following, everything is working as intended.

Congratulations, Jasper! Your system call is functional. Run the command dmesg in the terminal and find out!

23 - Check the last line of the dmesg output.
dmesg
At the bottom, you should now see the following.

![15](https://user-images.githubusercontent.com/85532323/121237449-5c5abf00-c897-11eb-8844-f3f7ccd7bf48.jpg)

References :
https://dev.to/jasper/adding-a-system-call-to-the-linux-kernel-5-8-1-in-ubuntu-20-04-lts-2ga8
https://medium.com/anubhav-shrimal/adding-a-hello-world-system-call-to-linux-kernel-dad32875872





