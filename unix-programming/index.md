# Unix Programming


# Unix Programming

## Bash

- Shortcuts

|     Function     | Shortcuts |       Help        |
| :--------------: | :-------: | :---------------: |
| previous Command | CTRL + p  |     previous      |
|   next Command   | CTRL + n  |       next        |
|   move forward   | CTRL + f  |   move forward    |
|  move backward   | CTRL + b  |  move backwoard   |
|       Del        | CTRL + d  |      delete       |
|       Home       | CTRL + a  | move to the Begin |
|       End        | CTRL + e  |  move to the End  |

## Directories in UNIX

- `/` root Directory
  - `/bin` executable Programms, like Commands
  - `/boot` Kernerl and Initialization Programms
  - `/dev` Devices
  - `/etc` Config and Startup Files
  - `/home` User's main Directory 
  - `/lib` Library Files for System Programms
  - `/media` media Devices like CD-ROM, USB Stick
  - `/mnt` Temporate Mount-System
  - `/proc` Memopry's Map
  - `/sbin` Super User executable Programms
  - `/usr`
    - `/usr/bin` executable Programms / Applications
    - `/usr/game`

## Some often-used Commands

### Link

- `ln -s <Source> <Your_Link_Name>` create a soft Link. Without the `-s` Parameter a hard Link will be created.

### Search
  
  - `find <Search_Directory> -name <File_Name>`
  
  - `grep <Pattern> <Search_Directory>`

### apt

- Change Source
    
  edit the file `/etc/apt/source.list`

- search Software

  `sudo apt-cache search package`

- fix the Installation

  `sudo apt-get -f install`

- install relative compile Enviroment
  
  `sudo apt-get build-dep package`

- upgrade the System

  `sudo apt-get dist-upgrade`

- get to know Depends

  `sudo apt-cache depends package`

### dpkg

- uninstall

  `sudo dpkg -r --purge xxx.deb`

- get Infos

  `sudo dpkg -info xxx.deb`

- show installed

  `sudo dpkg -l`

### devices

1. get Infos about Disks

    `sudo fdisk -l`

2. mount the Disk

    `mount <Device_Name> <Aim-Directory>`

3. unmount the Disk

    `umount <Aim-Directory>`

4. copy

    `dd if=<InputFile> of=<OutputFile> [bs=<File_Size> count=<Block_Size>]`

### compressed Files

#### tar

1. compress

    `tar cvf <.tar File> <Source>`

2. decompress

    `tar xvf <.tar File> [-C <Aim-Directory>]`

#### tar.gz

1. compress

    `tar zcvf <.tar.gz File> <Source>`

2. decompress

    `tar zxvf <.tar.gz File> [-C <Aim-Directory>]`

#### tar.bz2

1. compress

    `tar jcvf <.tar.bz2 File> <Source>`

2. decompress

    `tar -jxvf <.tar.bz2 File> [-C <Aim-Directory>]`

#### rar

1. compress

    `rar a -r <.rar File> <Directory_Name>`

2. decompress

    `unrar x <.rar File>`

#### zip

1. compress

    `zip -r <.zip File> <Directory>`

2. decompress

    `unzip <.zipFile>`
  
### Process

#### ps

1. `ps aux`

2. `ps ajx`

3. `ps -Lf`

#### kill

`kill [ -signal| -s signal ] pid ...`

`kill -l`

### env

- `env` check the Environment

- add new `$PATH`:
  
  - for self, `export PATH=$PATH:<path>` in `~/.bashrc`
  
  - for all users, `export PATH=$PATH:<path>` in `/etc/profile`

### Networks

- Info of Netcard 

  `ifconfig`

- shutdown Netcard

  `sudo ifconfig eth0 down`

- start Netcard

  `sudo ifconfig eth0 up`

- assign temporary IP

  `sudo ifconfig eth0 IP`

- Status of Network

  `netstat`

- transform WWW to IP

  `nslookup`
