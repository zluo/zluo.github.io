---
layout: default
title:  Linux Notes
nav_order: 1
parent: Linux Command
---

## Linux Note

1. TOC
{:toc}


## 1. Basic
### 1.1 Redirect
#### 1.1.1 Redircect both error stream and standard stream to a single file

    > file   Redirects stdout to file
    1> file  Redirects stdout to file
    2> file  Redirects stderr to file
    &> file  Redirects stdout and stderr to file

- stdout = 1
- stderr = 2
- stdout and stderr = &

The classic redirection operator (command > file) only redirects standard output, so standard error is still shown on the terminal. 
To redirect stderr as well, you have a few choices:

. Redirect stdout to one file and stderr to another file:

```bash
    command > out.log 2>error.log
```

. Redirect stderr to stdout (&1), and then redirect stdout to a file:

    command > out 2>&1

. Redirect both to a file:

    command &> out.log

#### 1.1.2 /dev/null
**/dev/null** treated as black hole.

. Run command in background, discard stdout and stderr

```bash
   command &> /dev/null &
```

{:.note }
first & means stdout and stderr, second & means run in background

. Run command in background and redirect stdout and redirect stdout and stderr to log file**

```bash
  command &>> /path/log &
  command >> /path/log 2>&1 &
```

#### 1.1.3. Redirect to mutilple output
**tee** - copy standard input to each file and also to standard output.

```bash
   ls -lrt | tee xyz
```

#### 1.1.4. remote write to a file


```bash
    echo 'Some Text' | ssh user@remotehost "cat > /remotefile.txt"
```

{:.note }
equivalent to scp

### 1.2 Directory Navigation

- Go to previous directory

```bash
    cd -
```
- Go to $HOME directory

```bash
    cd ~
```
- Go to dir, execute command and return to current dir

```bash
    cd dir && command
```
- Put current dir on stack so you can popd back to it

```bash
    pushd .
    dirs
    cd ~1
    cd ~2
```
## 2. List File (see Understating ls Notes)

### 2.1 create softlink

```bash
    ln -s /path/to/file /path/to/symlink
```

{:.note }
first parameter is source, second parameter is target


### 2.2 find softlink

```bash
    find  . -type l -ls
    ls -lR /path/to/folder | grep ^l
```

{:.note }
-R recursive

### 2.3. List files by date

```bash
  ls –lrt
    -l use a long listing format
    -r reverse order while shorting
    -t sort by time
```

### 2.4 List Tree

```bash
   ls -R | grep ":$" | sed -e 's/:$//' -e 's/[^-][^\/]*\//--/g' -e 's/^/   /' -e 's/-/|/'

   -R recurring
   -r reverse sort
```
### 2.5 Finding large files 

```bash
   find . -type f -size +10000 -exec ls -lrt {} \; | sort -n +4
```

#### 2.5.1 Use the *-xdev* option of find so as not to traverse devices...

```bash
   find / -xdev -type f -size +10000 -print | xargs du -ka | sort -rn
```

Sometimes use 
    
```bash
    du -kx|sort -n
```

On linux, following is the possible command:

```bash
    find / -type f -size +20000k -exec ls -lh {} \; | awk '{ print $9 ": " $5 }'
```

To tweak the output and have the file sizes in a column, add this to the end:

```bash
    | column -t
```
this just expands the tabs to even the columns out.





### 2.5.2 Finding all large directories

```bash
    find / -type d -size +50k
```


### 2.5.3 Find all files larger then ~10MB

```bash
    find / -size +10240000c -exec du -h {} \;
```

### 2.6. Only List Directory

```bash
    ls -ld */ .*/
    find –maxdepth 1 –type d
```

### 2.7  umask

set file and directory permission. 022

### 2.8      Accident press ctrl+s issue

```bash
ctrl+s lock screen, ctrl +q unlock
```

### 2.9   Cut

 ```bash
 cut -d ' ' -f 1 filename      get first colume of the output file.
 ```

### 2.11 Display command history

```bash
history
```

### 2.12 Run History command

```bash
!<history num>
```

### 2.13 Delete all folders and all files inside the folder.
    
```bash
    rm –R *
```
    
### 2.14 add user to group

- Add User

```bash
useradd -G {group-name} username
```
- Delete User

```bash
userdel username
```

Details see  Howto.Linux add user to group.doc

### 2.15 Tar – compress and extract files

#### 2.15.1    To create a Tar file

- Creates a GZIP-compressed Tar file of the name archive.tar.gz of all files with a .txt suffix.

```bash
     tar -cvzf archive.tar.gz *.txt
```
    -c create file
    -z gzip
    -f file

- compress whole folder

```bash
    tar -zvcf g10m.tar.gz /home/zluo/f/g10m
    gzip archive.tar
```

#### 2.15.2 To list files in a compressed Tar file

```bash
    tar -tvzf archive.tar.gz
    -t list
```
#### 2.15.3 To extract files from a Tar file

- Extracts all files from a compressed Tar file of the name archive.tar.gz.

```bash
    tar -xvzf archive.tar.gz
    -x extract
```

-  To extract to a specific folder

```bash
tar -xzf archive.tar.gz -C ~/dest/
```
-C directory

### 2.16 List open files
```bash
    lsof
```
### 2.17	Clean machine
 
Fsck – check and repair a Linux file system, need umount the file system first.

```bash
fsck -Y > /dev/null
```
 
{:.note }
/dev/null : no output



## 3.  Find and Search

### 3.1 find all java files, statistic the number of files

```bash
    find -name *.java | wc -l
    wc -l    counts the lines
```

### 3.2 find all java file, then find Exceptions in these files

```bash
    find -name *.java |xargs grep Exception
```

{:.note }
xargs, send multiple parameters to the grep


### 3.3 xargs, 

build and execute command lines from standard input, convert it into a command argument for another command.

### 3.4  Grep two strings

```bash
grep “dm-0\|sda”
```




## 4. Sed stream editor

```bash
   sed s/day/night/ < old.file > new.file
```

{:.note }
**s** for substitution;
**/** slash as a delimiter. (|,_ also can be a delimiter)

### 4.1 using & as the matched string

```bash
    sed 's/[a-z]*/(&)/
```

### 4.2  using \1 to keep part of the pattern

```bash
    $ echo 'abcabcabc' | sed 's/\(ab\)c/\1/'
    ababcabc
    $ echo 'abcabcabc' | sed 's/\(ab\)c/\1/g'
    ababab
    $ echo 'abcabcabc' | sed 's/\(ab\)\(c\)/\1d\2/g'
    abdcabdcabdc
```
### 4.3 sed examples
- Replace string1 with string2
```bash
sed 's/string1/string2/g'
```

- Modify anystring1 to anystring2
```bash
sed 's/\(.*\)1/\12/g'
```

- Remove comments and blank lines
```bash
sed '/ *=/d; /^ *$/d'
```
- Concatenate lines with trailing \
```bash
sed ':a; /\\$/N; s/\\\n//; ta'
```

- Remove trailing spaces from lines
```bash
sed 's/[ \t]*$//'
```

- Escape shell metacharacters active within double quotes
```bash
sed 's/\([\\`\\"$\\\\]\)/\\\1/g'
```

- Right align numbers
```bash
seq 10 | sed "s/^/      /; s/ *\(.\{7,\}\)/\1/"
```

- Print 1000th line
```bash
sed -n '1000p;1000q'
```

- Print lines 10 to 20
```bash
sed -n '10,20p;20q'
```

- Extract title from HTML web page
```bash
sed -n 's/.*<title>\(.*\)<\/title>.*/\1/ip;T;q'
```



## 5. Secure Copy (scp)

### 5.1 What is Secure Copy?
scp allows files to be copied to, from, or between different hosts. It uses ssh for data transfer and provides the same authentication and same level of security as ssh.

### 5.2 scp Examples

- Copy the file "foobar.txt" from a remote host to the local host

```bash
$ scp your_username@remotehost.edu:foobar.txt /some/local/directory
```

- Copy the file "foobar.txt" from the local host to a remote host
```bash
$ scp foobar.txt your_username@remotehost.edu:/some/remote/directory
```

- Copy the directory "foo" from the local host to a remote host's directory "bar"
```bash
$ scp -r foo your_username@remotehost.edu:/some/remote/directory/bar
```
Copy the file "foobar.txt" from remote host "rh1.edu" to remote host "rh2.edu"silanis1

$ scp your_username@rh1.edu:/some/remote/directory/foobar.txt \
your_username@rh2.edu:/some/remote/directory/
Copying the files "foo.txt" and "bar.txt" from the local host to your home directory on the remote host
$ scp foo.txt bar.txt your_username@remotehost.edu:~
Copy multiple files from the remote host to your current directory on the local host
$ scp your_username@remotehost.edu:/some/remote/directory/\{a,b,c\} .

$ scp your_username@remotehost.edu:~/\{foo.txt,bar.txt\} .

scp Performance
By default scp uses the Triple-DES cipher to encrypt the data being sent. Using the Blowfish cipher has been shown to increase speed. This can be done by using option -c blowfish in the command line.
$ scp -c blowfish some_file your_username@remotehost.edu:~
It is often suggested that the -C option for compression should also be used to increase speed. The effect of compression, however, will only significantly increase speed if your connection is very slow. Otherwise it may just be adding extra burden to the CPU. An example of using blowfish and compression:
$ scp -c blowfish -C local_file your_username@remotehost.edu:~
 

Example of wget copy

wget ftp://root:silanis1@10.0.1.229/space/home/aws40/test.txt

wget -r ftp://root:silanis1@10.0.1.229/space/home/aws40


Set up environment variable and alias in ~/.bashrc

= .bashrc
 
= User specific aliases and functions
 
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
 
= Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
 
appsrv01=/opt/WebSphere/AppServer/profiles/AppSrv01; export appsrv01
distribution=$appsrv01/distribution; export distribution
cache=$appsrv01/cache; export cache
log=$appsrv01/logs/server1; export log
log2=$appsrv01/logs/server2; export log2
 
alias clean='cd $distribution; rm * -rf; cd $cache; rm * -rf; cd $log; rm * -f;cd $log2; rm * -f'
alias lessout='cd $log; less SystemOut.log'
alias cleancache='cd $distribution; rm * -rf; cd $cache; rm * -rf'
alias taalias lesserr='cd $log; less SystemErr.log'
ilout='cd $log; tail -f SystemOut.log'
alias tailerr='cd $log; less -f SystemErr.log'
 
alias lessout2='cd $log2; less SystemOut.log'
alias lesserr2='cd $log2; less SystemErr.log'
alias tailerr2='cd $log2; less -f SystemErr.log'
alias tailout2='cd $log2; tail -f SystemOut.log'
 
 
 
alias mysmb='smbclient //zluo/temp -U sillsnis.com/zluo'
alias tailtrace='cd $log; tail -f trace.log'
 
alias collect='cd ~;grep Average rhelserver2.txt >rhelserver2_average.txt; smbclient //zluo/Test_Report bafosura -U silanis.com/zluo'
alias lesstrace='cd $log; less trace.log'
 
alias stopsv='cd $appsrv01/bin; ./stopServer.sh server1'
 
alias startsv='cd $appsrv01/bin; ./startServer.sh server1'
 
alias startnd='cd $appsrv01/bin; ./startNode.sh'
alias stopnd='cd $appsrv01/bin; ./stopNode.sh'
 
alias startmq='strmqm AWS_QM; runmqlsr -t tcp -m AWS_QM&'appsrv01=/opt/IBM/WebSphere/AppServer/profiles/AppSrv01; export appsrv01
distribution=$appsrv01/distribution; export distribution
cache=$appsrv01/cache; export cache
log=$appsrv01/logs/server1; export log
 
alias clean='cd $distribution; rm * -rf; cd $cache; rm * -rf; cd $log; rm * -f'
alias lessout='cd $log; less SystemOut.log'
alias lesserr='cd $log; less SystemErr.log'
 
alias tailout='cd $log; tail -f SystemOut.log'
alias tailerr='cd $log; less -f SystemErr.log'
alias mysmb='smbclient //zluo/temp bafosura -U silanis.com/zluo'
 
alias collectb='cd ~;grep Average rhelserver3.txt >rhelserver3_average.txt; smbclient //Test_Report bafosura -U silanis.com/zluo'


  
Command
Description
apropos whatis
Show commands pertinent to string. See also threadsafe
man -t man | ps2pdf - > man.pdf
make a pdf of a manual page
which command
Show full path name of command
time command
See how long a command takes
time cat
Start stop watch. Ctrl-d to stop. See also sw
nice info
Run a low priority command (The "info" reader in this case)
renice 19 -p $$
Make shell (script) low priority. Use for non interactive tasks



##  File Searching


alias l='ls -l --color=auto'
quick dir listing
ls -lrt
List files by date. See also newest and find_mm_yyyy
ls /usr/bin | pr -T9 -W$COLUMNS
Print in 9 columns to width of terminal
find -name '*.[ch]' | xargs grep -E 'expr'
Search 'expr' in this dir and below. See also findrepo
find -type f -print0 | xargs -r0 grep -F 'example'
Search all regular files for 'example' in this dir and below
find -maxdepth 1 -type f | xargs grep -F 'example'
Search all regular files for 'example' in this dir
find -maxdepth 1 -type d | while read dir; do echo $dir; echo cmd2; done
Process each item with multiple commands (in while loop)
find -type f ! -perm -444
Find files not readable by all (useful for web site)
find -type d ! -perm -111
Find dirs not accessible by all (useful for web site)
locate -r 'file[^/]*\.txt'
Search cached index for names. This re is like glob *file*.txt
look reference
Quickly search (sorted) dictionary for prefix
grep --color reference /usr/share/dict/words
Highlight occurances of regular expression in dictionary

##= Archives and Compression


. Encrypt file

    gpg -c file

. Decrypt file

    gpg file.gpg

. Make compressed archive of dir/

    tar -c dir/ | bzip2 > dir.tar.bz2

. Extract archive (use gzip instead of bzip2 for tar.gz files)

    bzip2 -dc dir.tar.bz2 | tar -x

. Make encrypted archive of dir/ on remote machine

    tar -c dir/ | gzip | gpg -c | ssh user@remote 'dd of=dir.tar.gz.gpg'

. Make archive of subset of dir/ and below

    find dir/ -name '*.txt' | tar -c --files-from=- | bzip2 > dir_txt.tar.bz2

. Make copy of subset of dir/ and below

    find dir/ -name '*.txt' | xargs cp -a --target-directory=dir_txt/ --parents

. Copy (with permissions) copy/ dir to /where/to/ dir

    ( tar -c /dir/to/copy ) | ( cd /where/to/ && tar -x -p )

. Copy (with permissions) contents of copy/ dir to /where/to/

    ( cd /dir/to/copy && tar -c . ) | ( cd /where/to/ && tar -x -p )

( tar -c /dir/to/copy ) | ssh -C user@remote 'cd /where/to/ && tar -x -p'
Copy (with permissions) copy/ dir to remote:/where/to/ dir
dd bs=1M if=/dev/sda | gzip | ssh user@remote 'dd of=sda.gz'
Backup harddisk to remote machine
rsync (Use the --dry-run option for testing)


rsync -P rsync://rsync.server.com/path/to/file file
Only get diffs. Do multiple times for troublesome downloads
rsync --bwlimit=1000 fromfile tofile
Locally copy with rate limit. It's like nice for I/O
rsync -az -e ssh --delete ~/public_html/ remote.com:'~/public_html'
Mirror web site (using compression and encryption)
rsync -auz -e ssh remote:/dir/ . && rsync -auz -e ssh . remote:/dir/
Synchronize current directory with remote one
ssh (Secure SHell)


ssh $USER@$HOST command
Run command on $HOST as $USER (default command=shell)
ssh -f -Y $USER@$HOSTNAME xeyes
Run GUI command on $HOSTNAME as $USER
scp -p -r $USER@$HOST: file dir/
Copy with permissions to $USER's home directory on $HOST
ssh -g -L 8080:localhost:80 root@$HOST
Forward connections to $HOSTNAME:8080 out to $HOST:80
ssh -R 1434:imap:143 root@$HOST
Forward connections from $HOST:1434 in to imap:143
wget (multi purpose download tool)


(cd cmdline && wget -nd -pHEKk http://www.pixelbeat.org/cmdline.html)
Store local browsable version of a page to the current dir
wget -c http://www.example.com/large.file
Continue downloading a partially downloaded file
wget -r -nd -np -l1 -A '*.jpg' http://www.example.com/dir/
Download a set of files to the current directory
wget ftp://remote/file[1-9].iso/
FTP supports globbing directly
wget -q -O- http://www.pixelbeat.org/timeline.html | grep 'a href' | head
Process output directly
echo 'wget url' | at 01:00
Download url at 1AM to current dir
wget --limit-rate=20k url
Do a low priority download (limit to 20KB/s in this case)
wget -nv --spider --force-html -i bookmarks.html
Check links in a file
wget --mirror http://www.example.com/
Efficiently update a local copy of a site (handy from cron)
networking (Note ifconfig, route, mii-tool, nslookup commands are obsolete)




ethtool eth0
Show status of ethernet interface eth0
ethtool --change eth0 autoneg off speed 100 duplex full
Manually set ethernet interface speed
iwconfig eth1
Show status of wireless interface eth1
iwconfig eth1 rate 1Mb/s fixed
Manually set wireless interface speed
iwlist scan
List wireless networks in range
ip link show
List network interfaces
ip link set dev eth0 name wan
Rename interface eth0 to wan
ip link set dev eth0 up
Bring interface eth0 up (or down)
ip addr show
List addresses for interfaces
ip addr add 1.2.3.4/24 brd + dev eth0
Add (or del) ip and mask (255.255.255.0)
ip route show
List routing table
ip route add default via 1.2.3.254
Set default gateway to 1.2.3.254
tc qdisc add dev lo root handle 1:0 netem delay 20msec
Add 20ms latency to loopback device (for testing)
tc qdisc del dev lo root
Remove latency added above
host pixelbeat.org
Lookup DNS ip address for name or vice versa
hostname -i
Lookup local ip address (equivalent to host `hostname`)
whois pixelbeat.org
Lookup whois info for hostname or ip address
netstat -tupl
List internet services on a system
netstat -tup
List active connections to/from system
windows networking (Note samba is the package that provides all this windows specific networking support)


smbtree
Find windows machines. See also findsmb
nmblookup -A 1.2.3.4
Find the windows (netbios) name associated with ip address
smbclient -L windows_box
List shares on windows machine or samba server
mount -t smbfs -o fmask=666,guest //windows_box/share /mnt/share
Mount a windows share
echo 'message' | smbclient -M windows_box
Send popup to windows machine (off by default in XP sp2)
text manipulation (Note sed uses stdin and stdout, so if you want to edit files, append <oldfile >newfile)


sort -t. -k1,1n -k2,2n -k3,3n -k4,4n
Sort IPV4 ip addresses
echo 'Test' | tr '[:lower:]' '[:upper:]'
Case conversion
tr -dc '[:print:]' < /dev/urandom
Filter non printable characters
history | wc -l
Count lines
set operations (Note you can export LANG=C for speed. Also these assume no duplicate lines within a file)


sort file1 file2 | uniq
Union of unsorted files
sort file1 file2 | uniq -d
Intersection of unsorted files
sort file1 file1 file2 | uniq -u
Difference of unsorted files
sort file1 file2 | uniq -u
Symmetric Difference of unsorted files
join -a1 -a2 file1 file2
Union of sorted files
join file1 file2
Intersection of sorted files
join -v2 file1 file2
Difference of sorted files
join -v1 -v2 file1 file2
Symmetric Difference of sorted files
math


echo '(1 + sqrt(5))/2' | bc -l
Quick math (Calculate φ). See also bc
echo 'pad=20; min=64; (100*10^6)/((pad+min)*8)' | bc
More complex (int) e.g. This shows max FastE packet rate
echo 'pad=20; min=64; print (100E6)/((pad+min)*8)' | python
Python handles scientific notation
echo 'pad=20; plot [64:1518] (100*10**6)/((pad+x)*8)' | gnuplot -persist
Plot FastE packet rate vs packet size
echo 'obase=16; ibase=10; 64206' | bc
Base conversion (decimal to hexadecimal)
echo $((0x2dec))
Base conversion (hex to dec) ((shell arithmetic expansion))
units -t '100m/9.74s' 'miles/hour'
Unit conversion (metric to imperial)
units -t '500GB' 'GiB'
Unit conversion (SI to IEC prefixes)
units -t '1 googol'
Definition lookup
seq 100 | (tr '\n' +; echo 0) | bc
Add a column of numbers. See also add and funcpy
calendar


cal -3
Display a calendar
cal 9 1752
Display a calendar for a particular month year
date -d fri
What date is it this friday. See also day
date --date='25 Dec' +%A
What day does xmas fall on, this year
date --date '1970-01-01 UTC 2147483647 seconds'
Convert number of seconds since the epoch to a date
TZ=':America/Los_Angeles' date
What time is it on West coast of US (use tzselect to find TZ)
echo "mail -s 'get the train' P@draigBrady.com < /dev/null" | at 17:45
Email reminder
echo "DISPLAY=$DISPLAY xmessage cooker" | at "NOW + 30 minutes"
Popup reminder
locales


printf "%'d\n" 1234
Print number with thousands grouping appropriate to locale
BLOCK_SIZE=\'1 ls -l
get ls to do thousands grouping appropriate to locale
echo "I live in `locale territory`"
Extract info from locale database
LANG=en_IE.utf8 locale int_prefix
Lookup locale info for specific country. See also ccodes
locale | cut -d= -f1 | xargs locale -kc | less
List fields available in locale database
recode (Obsoletes iconv, dos2unix, unix2dos)


recode -l | less
Show available conversions (aliases on each line)
recode windows-1252.. file_to_change.txt
Windows "ansi" to local charset (auto does CRLF conversion)
recode utf-8/CRLF.. file_to_change.txt
Windows utf8 to local charset
recode iso-8859-15..utf8 file_to_change.txt
Latin9 (western europe) to utf8
recode ../b64 < file.txt > file.b64
Base64 encode
recode /qp.. < file.txt > file.qp
Quoted printable decode
recode ..HTML < file.txt > file.html
Text to HTML
recode -lf windows-1252 | grep euro
Lookup table of characters
echo -n 0x80 | recode latin-9/x1..dump
Show what a code represents in latin-9 charmap
echo -n 0x20AC | recode ucs-2/x2..latin-9/x
Show latin-9 encoding
echo -n 0x20AC | recode ucs-2/x2..utf-8/x
Show utf-8 encoding
CDs


gzip < /dev/cdrom > cdrom.iso.gz
Save copy of data cdrom
mkisofs -V LABEL -r dir | gzip > cdrom.iso.gz
Create cdrom image from contents of dir
mount -o loop cdrom.iso /mnt/dir
Mount the cdrom image at /mnt/dir (read only)
cdrecord -v dev=/dev/cdrom blank=fast
Clear a CDRW
gzip -dc cdrom.iso.gz | cdrecord -v dev=/dev/cdrom -
Burn cdrom image (use dev=ATAPI -scanbus to confirm dev)
cdparanoia -B
Rip audio tracks from CD to wav files in current dir
cdrecord -v dev=/dev/cdrom -audio *.wav
Make audio CD from all wavs in current dir (see also cdrdao)
oggenc --tracknum='track' track.cdda.wav -o 'track.ogg'
Make ogg file from wav file
disk space (See also FSlint)


ls -lSr
Show files by size, biggest last
du -s * | sort -k1,1rn | head
Show top disk users in current dir. See also dutop
df -h
Show free space on mounted filesystems
df -i
Show free inodes on mounted filesystems
fdisk -l
Show disks partitions sizes and types (run as root)
rpm -q -a --qf '%10{SIZE}\t%{NAME}\n' | sort -k1,1n
List all packages by installed size (Bytes) on rpm distros
dpkg-query -W -f='${Installed-Size;10}\t${Package}\n' | sort -k1,1n
List all packages by installed size (KBytes) on deb distros
dd bs=1 seek=2TB if=/dev/null of=ext3.test
Create a large test file (taking no space). See also truncate
monitoring/debugging


tail -f /var/log/messages
Monitor messages in a log file
strace -c ls >/dev/null
Summarise/profile system calls made by command
strace -f -e open ls >/dev/null
List system calls made by command
ltrace -f -e getenv ls >/dev/null
List library calls made by command
lsof -p $$
List paths that process id has open
lsof ~
List processes that have specified path open
tcpdump not port 22
Show network traffic except ssh. See also tcpdump_not_me
ps -e -o pid,args --forest
List processes in a hierarchy
ps -e -o pcpu,cpu,nice,state,cputime,args --sort pcpu | sed '/^ 0.0 /d'
List processes by % cpu usage
ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS
List processes by mem usage. See also ps_mem.py
ps -C firefox-bin -L -o pid,tid,pcpu,state
List all threads for a particular process
ps -p 1,2
List info for particular process IDs
last reboot
Show system reboot history
free -m
Show amount of (remaining) RAM (-m displays in MB)

**Watch changeable data continuously**
<pre>watch -n1 'cat /proc/interrupts'</pre>

system information (see also sysinfo) ('=' means root access is required)


uname -a
Show kernel version and system architecture
head -n1 /etc/issue
Show name and version of distribution
cat /proc/partitions
Show all partitions registered on the system
grep MemTotal /proc/meminfo
Show RAM total seen by the system
grep "model name" /proc/cpuinfo
Show CPU(s) info
lspci -tv
Show PCI info
lsusb -tv
Show USB info
mount | column -t
List mounted filesystems on the system (and align output)
dmidecode -q | less
Display SMBIOS/DMI information
smartctl -A /dev/sda | grep Power_On_Hours
How long has this disk (system) been powered on in total
hdparm -i /dev/sda
Show info about disk sda
hdparm -tT /dev/sda
Do a read speed test on disk sda
badblocks -s /dev/sda
Test for unreadable blocks on disk sda
interactive (see also linux keyboard shortcuts)


readline
Line editor used by bash, python, bc, gnuplot, ...
screen
Virtual terminals with detach capability, ...
mc
Powerful file manager that can browse rpm, tar, ftp, ssh, ...
gnuplot
Interactive/scriptable graphing
links
Web browser
miscellaneous


alias hd='od -Ax -tx1z -v'
Handy hexdump. (usage e.g.: • hd /proc/self/cmdline | less)
alias realpath='readlink -f'
Canonicalize path. (usage e.g.: • realpath ~/../$USER)
set | grep $USER
Search current environment
touch -c -t 0304050607 file
Set file timestamp (YYMMDDhhmm)
 
3         System Imager
3.1      Download the required packages
 

 $ mkdir systemimager
 $ cd systemimager
 $ wget http://download.systemimager.org/pub/sis-install/install
 $ chmod u+x install
 

 
Wget get the install from the URL.
chmod u+x
 
u Sets permissions for the owner of the file.
 

$ ./install -v --download-only --tag stable --directory . systemconfigurator \
 > systemimager-client systemimager-common \
 > systemimager-i386boot-standard systemimager-i386initrd_template \
 > systemimager-server \
 > systemimager-bittorrent systemimager-flamethrower

 
\ means link mulitline.
 
 
Also need download:
 

 perl-AppConfig-1.52-4.noarch.rmp
 perl-XML-Simple-2.14-2.2.el4.rf.noarch.rpm

 
“noarch” simply means on any architecture.
3.2      Install server
 
 
 
3.3      Install client
 
 
 
3.4      Get Image
 
 
4         System Monitoring
4.1      Conception
4.1.1       Process
 
Process is an instance of execution that runs on a processor.
 
Life cycle of a process
 
Parent process -> Fork() child process -> exec() -> zombie process
 
Parent process clean zombie process.
 
4.1.2      Thread
Thread is an execution unit generated in a single process.
 
4.1.3       Process State
TASK_RUNNING
TASK_STOPPED
TASK_INTERUPTIBLE
TASK_UNINTERUPTIBLE
TASK_ZOMBIE
 
4.1.4       Process address space
 
 
4.2      Monitoring tools
 
 
 
CPU

sar –u

 
I/O

sar -b

 
 
 
 
 
 
 
 
 
Sar –ubr –n DEV 15 240 > serverName.txt
 
 
4.3      Iostat
 
 
5         X window System
4 components consist of X window system.
 
X server, X client, X protocol, X manager
5.1      Configuration
.xinitrc
 
 
5.2 xhost

Run the program in one host, but the GUI displayed in another host.

Example of Typical Use

localhost     128.100.2.6	    remotehost    17.200.10.5

1. on the localhost

% xhost + 17.200.10.5    (allow   17.200.10.5 to access X-server of localhost)

2.   log on the remote host

% telnet 17.200.10.5

3. On the remote host (through the telnet connection)

%setenv DISPLAY 128.100.2.16:0.0 (what's means of 0.0)  displayNumber(monitor and keyboard number).(screenNumber, windows number)

4. Now you can run software from the remote host

%xterm

see an xterm window on the localhost
 



Integrate Xserver with Windows
1. Install Xming on windows
Xming X-Server for Windows

2. Double click on the Xming shortcut on the desktop (see figure below)
   
Note: If a firewall installed,  will need to allow remote hosts access to the X-server
 

3. Launch Putty and enable X11 forwarding by enabling Enable X11 forwarding Tunnels options. 

4. Connect to the remote server through Puttye server from this workstation, you will be presented with a Security Alert, Click Yes (see figure below)

5.Next login and run a X-1 application. In this example we will run xterm or firefox (see figure below)



 
6         Create boot Disk
6.1      cpu info

/proc/cpuinfo

 
 
6.2      create a boot USB key
 
create image file
 

dd if=/media/disk/images/diskboot.img of=/dev/sdc

 
   2. record to CD ROOM
 

= cdrecord dev=/dev/hdc -v -eject /tmp/boot.iso

 
 
 
Remove CR character

Method 1: In Notepad ++ , replace '\r' .

command line: tr

tr command

change all lowcase character to Upcase character:

tr '[a-z]' '[A-Z]' < columns.txt > UpCaseColumns.txt

 
Combining Unix Command Using && and ||

 
command1 && command2,  means if command1 successful, then run command2
command2 || commands  will do the opposite, if the exit code is not true then run command2

example: 
    [-f filename1] && rm filename1
 

2.18Samba Client (see setup samba server)
usr/local/samba/bin/./smbclient //Zluo/temp -U silanis.com/zluoassword:
smb> recurse (toggle)
smb> prompt  (toggle)
smb> mput *
 
 

















2.1      CD/DVD backup
mkisofs -J -r -T -o /tmp/backhome.iso /home
 
= cdrecord -v /tmp/backhome.iso
 

 



Add Virtual Disk Group In Linux

create new partition on the disk.

fdisk /dev/sdc.
 
     2. Specify the partition type as 8e
      type t, specify the partition type. (8e) 

          
      2. This sets up physical extents and other things that LVM needs. The command we run is  "pvcreate /dev/sdc1"

Extend existing volume group onto new partition.
For this example we are going to assume that we have an existing volume group named rootvg. We can display information about this volume group using the vgdisplay command. If we type "vgdisplay" without any arguments, it will display all the volume groups. If we just want information about the "rootvg" volume group, we would type "vgdisplay rootvg".
To extend the rootvg volume group onto the new partition, we use the vgextend command. Type "vgextend rootvg /dev/sdc1" followed by the enter key. This will extend the rootvg volume group onto the new partition, /dev/sdc1.
Extend existing logical volume onto new space.
For this example we are going to assume that we have an existing logical volume on the rootvg volume group that is named homelv. The full path to this logical volume would be "/dev/rootvg/homelv". We can view information about this logical volume by typing "lvdisplay /dev/rootvg/homelv".
To extend this existing logical volume onto the new space we use the lvextend command. Type "lvextend -L +20G /dev/rootvg/homelv /dev/sdc1". This command says that we want to increase the /dev/rootvg/homelv logical volume by 20GB. This is only possible if /dev/sdc1 is a member of volume group rootvg and there is enough free disk space on it.
The last thing we need to do is increase the filesystem.
Which command we use to increase the filesystem depends on what filesystem type we are currently using. If we are using reiserfs, we will use the "resize_reiserfs" command. If we are using ext3, we will use either the "ext2online" or the "resize2fs" command. On RHEL 5, we can use the "resize2fs" command, which will recognize that the filesystem is currently mounted and perform an "on-line" resize.
On both resize_reiserfs and ext2online, the size is optional. If we want the filesystem to take up all the available space on our logical volume, we don't need to put the size. To extend the filesystem type either "ext2online /dev/rootvg/homelv" or "resize_reiserfs /dev/rootvg/homelv".



Redhat 5 related config commands

1. config hostname

system-config-network

2. config services

system-config-services


View Linux System Configuration

cat /proc/cpuinfo
cat /proc/meminfo


View Linux System Logs

cd /var/logs


/var/log/message: 
General message and system related stuff
/var/log/auth.log: 
Authenication logs
/var/log/kern.log: 
Kernel logs
/var/log/cron.log
Crond logs (cron job)


/var/log/maillog: Mail server logs


/var/log/qmail/
 Qmail log directory (more files inside this directory)
/var/log/httpd/
Apache access and error logs directory
/var/log/lighttpd: 
Lighttpd access and error logs directory
/var/log/boot.log 
System boot log
/var/log/mysqld.log
MySQL database server log file
/var/log/secure
Authentication log
/var/log/utmp or /var/log/wtmp  
Login records file
/var/log/yum.log
Yum log files



SSH without password

Install cygwin
Set up cygwin home match to windows home folder


 vi /etc/nsswitch.conf

Add a line 
    db_home: /%H 
  


Create keypairs

chmod 400 ~/.ssh/id_rsa



  ssh-copy-id root@remote-machine

     3. Ssh-add

eval $(ssh-agent)
ssh-add






####=

1. tar
2. display jpg
3. installl hts drive
4. mount / umount drive

    mount -t hfsplus -o force,rw /dev/sdc2 /media/zluo/G-FORCE

5. find device namesudo
6. find file name by size
7. find file and move file
8. meida commands
9. shell cript loop









Reference

1. xhost 
http://linux.about.com/library/cmd/blcmdl_xhost.htm
2. X server
http://www.comptechdoc.org/os/linux/howlinuxworks/linux_hlxwindows.html

3.Linux Tutorial
http://www.yolinux.com/TUTORIALS/LinuxTutorialSysAdmin.html=MONITOR




##= Test a user have permission to a directory

    sudo -u $user test -r /directory

    check $?

### Add a user
#### 1. Add a user

     sudo adduser <user>
#### 2. set password

     sudo passwd <user>
#### 3 Assign user's privilege

###### 3.1 add this user to a group
sudo usermod -aG <group> <user>

###### 3.2 Or visudo
sudo visudo

Linux File System Hierarchy and Structure (see Linux File System Notes)

Partition
fdsk   /dev/sda
format

Check Disk

    // partition

mkfs  -t ext3 /dev/hd2       // format

fsck  /dev/hda7       // check disk
2.6      Updatedb and locate
updatedb
locate
