+++
date = "2021-09-11T10:54:24+02:00"
draft = false
title = "Beginning Linux Kernel Development [ A simple module ]"
slug = "post-title"
tags = ["Linux","C","Kernel Development"]
image = ""
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = "Andrew"
+++

```

Linux Kernel Development is the process of writing code to run in the Kernel Space. 
It's one of the most important parts of a complex operating systems.

Device Drivers controls a particular device connected to the computer. 

I am going to dive into explaining 2 things:
1. A simple Hello World Kernel Module.
2. A character device driver.

Information about the Kernel is alot to compress into single writing and therefore I only try to explain my 1st 2 code pieces.

----> 1. Hello World, mymodule.c <----

//code begins here
#include<linux/module.h>
#include<linux/init.h>
#include<linux/fs.h>

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Andrew Mbugua");
MODULE_DESCRIPTION("Registers a device and implement some call back function");

/**@brief this function is called,when the device file is opened

 */
static int __init ModuleInit(void){

printk("Hello Kernel");
return 0;

}
/**
@This function is called when the module is removed from the kernel
*/

static void __exit ModuleExit(void){
printk("Goodbye, Kernel");

}

module_init(ModuleInit);
module_exit(ModuleExit);

// End of module

----> Create the a Makefile(a Makefile is responsible creating a build) <----

$ touch Makefile
$ vi Makefile


obj-m += mymodule.o

all:

         make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
        make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean


$ make

The following output is generated:

make -C /lib/modules/5.4.0-86-generic/build M=/home/kernel_dev_server modules
make[1]: Entering directory '/usr/src/linux-headers-5.4.0-86-generic'
  Building modules, stage 2.
  MODPOST 1 modules
make[1]: Leaving directory '/usr/src/linux-headers-5.4.0-86-generic'

multiple files will be generated,the main focus here will be the mymodule.ko,
an extension used for Kernel Modules.

----> loading the module <----

$ insmod mymodule.ko

# verify that it has been loaded

$ dmesg

This prints the information from the Kernel's ring buffer.

[  123.069922] Hello Kernel

----> Problems & error messages encountered and the solutions if you
 choose to dive into Kernel Development <----

### Problem 1:

ERROR: could not insert module /lib/modules/r1soft/hcpdriver-cki-XXX.ko: Operation not permitted 
 
### solution


Restarting the system is done if the memory becomes fragmented to a point where our memory request allocation is denied.


This article explains best the problem encountered at hand (https://bit.ly/3muMCUT)



```
