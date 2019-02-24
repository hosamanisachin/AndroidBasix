# AndroidBasix

1) Android OS Kernel
- It goes to sleep as frequent as possible.
- Only few key processes run in the background during sleep mode.
- It uses Wakelock on top of power manager to manage power.
- It uses Binder on its IPC mechanism.
- It uses ashmem(Async Shared Memory)
- Disk in android is flash(NAND Flash)
       File System *YAFFS v4.2.3 Android <2.3
                   *ext4 Android >2.3

How an Android device starts?
We have a Boot_ROM(is in the CPU) that needs to be run and it needs free electron space(i.e. RAM) to execute. Boot_ROM stores the address of boot_code which is present on the flash. 
Now we need to get this boot_code into RAM and start the execution.
The role of boot_code is to locate where the bootloader is (uBOOT-universal bootloader) and get it into the RAM.
Bootloader loads the kernel. Kernel calls the "init" process.
This "init" process starts "Zygote".
Zygote loads the Dalvik:- Its is JVM for Android {Uses 70% bytecode and 30% asm code; It is register based}

Why Dalvik in boot process?
- All application need JVM.
The zygote also loads system_server{Initialises all system services like Package Manager etc}
  *system_server is the first java application and therefore the reason for dalvik to be run in bootprocess.
  
- The Package Manager starts the Activity Manager, Service Manager etc.
- The Activity Manager starts system launcher i.e. it sends a broadcast message to all application saying boot_completed.
