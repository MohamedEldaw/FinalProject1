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

![4](https://user-images.githubusercontent.com/85532323/121233974-814d3300-c893-11eb-8ef5-bf5fccf37a7f.jpg)

2.Download and install the essential packages to compile kernels
sudo apt install build-essential libncurses-dev libssl-dev libelf-dev bison flex -y
![1](https://user-images.githubusercontent.com/85532323/121233519-ff5d0a00-c892-11eb-9167-bc5cdde6ad8d.jpg)

 3.Clean up your installed packages:
 sudo apt clean && sudo apt autoremove -y
 ![2](https://user-images.githubusercontent.com/85532323/121233668-24517d00-c893-11eb-9092-2199f6836197.jpg)

4.Download the source code of the latest stable version of the Linux kernel (which is 5.12.9 as of 12) to your home folder:
wget -P ~/ https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.12.9.tar.xz![3](https://user-images.githubusercontent.com/85532323/121233854-5d89ed00-c893-11eb-9a68-1e74ea815798.jpg)



5.Unpack the tarball you just downloaded to your home folder:
tar -xvf ~/linux-5.12.9.tar.xz -C ~/






