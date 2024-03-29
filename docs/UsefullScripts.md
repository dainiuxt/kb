# bash/shell

[bashcrawl](https://gitlab.com/slackermedia/bashcrawl)

> Learn Linux commands by playing a simple text adventure.

[Effective Shell](https://effective-shell.com/)

> This book is for anyone who is interested in computing, and wants to learn more about the exciting, but sometimes daunting world of The Shell. The shell is simple interface for working with computers and programs and learning some of its features can enormously increase your productivity as any computer user - whether a home user or hobbyist, programmer, data scientist, writer, administrator or other professional.
> 
> For the newcomer, you'll learn what a shell is, how to use it on your system, and then how to become more effective everyday by integrating the shell into your work. For the experienced professional, there is a wealth of detailed tips and tricks in each chapter that go into advanced topics and techniques to make you even more of a power user.


## Scripts & Commands

[Writing a `bash` scripts like a pro](https://dev.to/unfor19/writing-bash-scripts-like-a-pro-part-1-styling-guide-4bin)

Resize multiple graphic files from the command line:

```bash
sudo apt-get install imagemagick
mogrify -resize 640 *.jpg
```

Convert large jpg/png files into webp:

```bash
sudo apt-get install webp
cd /mywebapp/static/img/
mkdir webp        
for file in *.{jpg,png,jpeg}; do cwebp -q 60 ${file} -o webp/${file}.webp; done;
```

[Linux commands for optimizing web images](https://opensource.com/article/21/12/optimize-web-images-linux)


## Linux commands for advanced hardware info

[source](https://nixsanctuary.com/best-linux-hardware-system-info-commands/)

Sometimes you need info about hardware, and you probably lost your invoice, spec list or a password to a store website. Maybe you did an upgrade and this info isn't accurate anymore. It's an easy case for home users, but what to do is you have many machines in a corporate environment? The commands below will also be useful for hardware debug.

### `Uname` - Linux kernel info

`uname -a` - kernel version  
`uname -m` - system architecture

### `lspci` - list of all attached devices to PCI bus

`lspci -vvv` - enable verbose mode.

    # lspci
    00:00.0 Host bridge: Intel Corporation 5500 I/O Hub to ESI Port (rev 13)
    00:01.0 PCI bridge: Intel Corporation 5520/5500/X58 I/O Hub PCI Express Root Port 1 (rev 13)
    00:09.0 PCI bridge: Intel Corporation 7500/5520/5500/X58 I/O Hub PCI Express Root Port 9 (rev 13)
    

### `lshw` - complete `all in one` list of installed hardware components

`lshw` works without `sudo`, but provides much less info. Includes memory configuration, firmware revisions, CPU info and core frequencies. `--sanitize` flag is super useful when you want to upload result to the internet, it will hide IP addresses and serial numbers, `--short`flag is good for compact output.  
Report in HTML is very helpful for easy sharing: `$ sudo lshw –html > report.html`

### `hwinfo` - another tool, very similar to `lshw`

[Hwinfo](https://github.com/openSUSE/hwinfo), created by SUSE developers, is another general purpose hardware probing utility capable off reporting detailed and brief information about multiple different hardware components.  
Examples:

    $ hwinfo
    $ hwinfo –short
    

### `dmidecode` -extract info from BIOS/UEFI using SMBIOS API.

`--type` option for device-related info like `bios,system,chassis`

Examples:

    $ sudo dmidecode -t processor
    $ sudo dmidecode -t memory
    

### `lsusb` - perfect command to show all pluggable devices

Useful flags: `-vvv` for verbose mode, `-s [bus]:[devnum]` will show only specific device on you need to watch. You can easily sort by vendor with `-d [vendor]:[product]`, view all in three modes with `-t` and use device-file config with `-S /dev/X` option.

    $ lsusb
    Bus 005 Device 002: ID 045e:00cb Microsoft Corp. Basic Optical Mouse v2.0
    Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
    

### `lscpu` - first command to get CPU info

Verbose mode can be enabled with `-e` flag, `-p` also very useful for better formatting. `--online` and `--offline` can be specified for better visualization.

### `lsscsi` - print attacked SCSI devices into

"Old bud gold" SCSI drives used mostly in enterprise, more costly than PCI & SATA devices. Verbose mode can be enabled with `-L`, `-l` and `-v` options.

    $ lsscsi
    [3:0:0:0] disk ATA ST3500418AS CC38 /dev/sda
    [4:0:0:0] cd/dvd SONY DVD RW DRU-190A 1.63 /dev/sr0
    

### `dmesg` - kernel logs

Kernel logs are very helpful for hardware events like attach, detach, shutdown etc. Works much better with `grep` and `less` commands: `sudo dmesg | grep -i audio | less`.

### `inxi` - "all in one" script

The crazy, bigger than 10k lines of code, bash script, capable to fetch multiple system APIs and provide gigantic pile of info. Useful flags: `-z` to hide sensitive info if you wanna upload reports to internet, `-F` for verbose mode, `-A` for audio information, `-m` - memory, - `-i` - networking, `-p` - disk info, all options you can check in help menu which can be invoked by `-H`.

### `fdisk`, `gdisk` and `parted` - all about your drive partitions

Why are there three commands here, you want to ask? Well, they are doing very similar jobs and completely independent projects. `gdisk` was a `fdisk` fork with GTP partitioning mode support; now `fdisk` supports `GPT` too. Covering their options will take several posts like this, but here's how to check your drive info: `$ fdisk -l` or `gdisk -l` or `parted -l`.

### `blkid` and `lsblk` - block devices list

These commands shows info about available block devices. Examples below:

    $ lsblk -a
    NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
    sda 8:0 0 232.9G 0 disk
    ├─sda1 8:1 0 200M 0 part
    

    # blkid -i /dev/sda
    /dev/sda: MINIMUM_IO_SIZE="512" PHYSICAL_SECTOR_SIZE="512" LOGICAL_SECTOR_SIZE="512"
    

### `mount` - mount a drive and print info about already mounted

`$ mount | column -t` for better visualization, `sudo mount /dev/sdaN /media/data` - mount a partition.

    $ mount | column -t
    /dev/sda2   on  /                                type  ext4        (rw,relatime,stripe=256)
    devtmpfs    on  /dev                             type  devtmpfs    (rw,nosuid,noexec,relatime,size=5827492k,nr_inodes=1456873,mode=755,inode64)
    

### `df` - check used and free disk space

Useful flag: `df -H` - human-readable output.

### `/proc` - virtual file system full of hardware/software related info and configuration

`/prop/cpuinfo` - CPU specs  
`/proc/version` - kernel version  
`/proc/partitions` - partitions info

### `hdparm` - get/set SATA/IDE device parameters

Available by default in most of Linux distribution for many years, very useful for advanced configuration.

`$ hdparm -g` - display drive geometry

`$ hdparm -tT /dev/sdN` - partition reading & writing benchmark
