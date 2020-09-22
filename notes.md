#Processor type and features
##Compression
LZ4 compression is much faster than gzip compression in teory, it's worth to checking if the boot time differs
Maybe is worth to check XZ compression too (really high compression, but spends a lot of time, and uses a lot of memory, more than lz4 if compress in a lot of levels)
LZ4 uses more memory (12mb x 0.3mb), and compress less, but is much faster (5x/3x)

	https://catchchallenger.first-world.info/wiki/Quick_Benchmark:_Gzip_vs_Bzip2_vs_LZMA_vs_XZ_vs_LZ4_vs_LZO#Selected_archives
	https://linuxaria.com/article/linux-compressors-comparison-on-centos-6-5-x86-64-lzo-vs-lz4-vs-gzip-vs-bzip2-vs-lzma

	
##Posix
POSIX message queue
POSIX message queues allow processes to exchange data in the form of messages.
message queue is similar to a pipe
message queue i can know the state, pipe i can't
###Opinion
Looks like something better for real time systems, maybe i can disable that

	https://www.man7.org/linux/man-pages/man7/mq_overview.7.html
	
##proccess_vm_readv/writev
readv system call transfers data from remote process to local process
writev system call transfers data from local process to remote process
###Opinion
Don't know if it's worth it or beneficial remove it or not


	https://man7.org/linux/man-pages/man2/process_vm_readv.2.html
	https://man7.org/linux/man-pages/man2/process_vm_writev.2.html

##uselib syscall
Used if a program is compiled with libc5 or earlier
Aparrently most people uses glibc, so it can be turned off
###glibc vs libc5
libc5 and earlier were versions of the Linux C library, which was originally based on the GNU C Library 1
libc6 is equal to glibc apparently
libc5 is apparently very outdated (1998 post saying that, so... kkkkkkk)

	Gentoo module help
	https://www.linux.co.cr/lg/issue32/tag_libc5.html
	https://arstechnica.com/civis/viewtopic.php?t=1000076 (forum)
	https://www.linux.co.cr/lg/issue32/tag_libc5.html (1998 chat with HJ Lu)

##Auditing support
Looks like some logging module
the forum said that it's slow down de notebook

	https://www.linuxquestions.org/questions/linux-newbie-8/what-is-auditing-support-349602/
	https://wiki.archlinux.org/index.php/Audit_framework

##Timers config
The video changes de timer policy to a periodic timer tick (which makes the clock with stable freq), this option uses more energy, but can increase performance
After that, disable the 2 other options that are related to a tickeless idle
	
	Gentoo module help

##CPU/Task time and stats accounting
###BSD Process Accounting
It adds information about the system, if disabled, some task managers like htop may fail
Don't found if it can reduce cpu overhead
###Export task/process statistics through netlink
"Unlike BSD process accounting, the statistics are available during the lifetime of task/process"

	Gentoo Module help

##Kernel log buffer size and CPU kernel log buffer size and Temporary per=CPU printk log buffer size
Need to do a good research to see if a good size

##Initramfs
but i don't know the effectiveness of that action

#Processor type and features
##Enable MPS table
Only needed in older systems (not needed in esp with 64bits cpus)

	Gentoo module help

##Support for extended (non-PC) x86 platforms
if disabled, kernel will only support standard pc platforms (vast majority)
this option adds support for Numascale NumaChip, ScaleMP vSMP, SGI Ultraviolet

	Gentoo module help

##Maximum number of CPUs
Just saves memory, adds 8KB for every CPU added in image

	Gentoo module help

##Multi-core scheduler support
Adds support to CPU scheduler's decision
slightly increase overhead

	Gentoo module help

##Rerout for brojen boot IRQs
need do search, it's look like complex
the video says it works only for old cpu

##Some options for Intel and AMD and MAC architeture are set too by default

##Enable 5-level page tables support
Add suport for larger address space: 128PiB of virtual address, and 4PiB of physical address space
Don't know any PC with this space kkkkkkk

##Numa Memory Allocation and Scheduler Support
The video say that It's work for CPU with more than 16 threads
The gentoo module help says it should be abled only with i7 core or later

##Check for low memory corruption
Check memory corruption on BIOS level
Even though it appears to be very rare, it says that almost has no overhead, and reserver relatively small amount of memory

##MTRR cleanup support
It's related to X display server, "if unsure say yes" said the gentoo module help

##Inter Memory Protection Keys
need to search more about, does not say about the overhead

##kexec system call
It enable kernel change quickly
###kernel crash dumps
Module related to kexec, need to search more about it
###Build a relocatable kernel
Another module related to kexec
it makes the kernel binary 10% larger
it helps in kernel panic with recovery kernel to boot in a different physical address

#Power management and ACPI options
##Suspend to ram and standby
need to search more about the module to see the effects
it is related to sleep mode, so maybe not necessary for desktops

##Hibernation
Also more related with notebooks than CPUs

##Power Management Debug Support
adds debugging suport

##Block layer debugging ingormation in debugfs
name is explicative
doesn't incur any cost at runtime

#PCCard support
nead to search more

##Number of loop devices to pre-create at init time
Static create loop devices
can be set to 0 to be created on demand

##Asynchronous SCSI scanning
can speed-up boot time
"Note that this setting also affects wheter resuming from system suspend will be performed asynchronously"

##RCU CPUP stall timeout in seconds
need to search more
