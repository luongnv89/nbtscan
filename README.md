# NBTscan

NBTscan is a program for scanning IP networks for NetBIOS name
information. It sends NetBIOS status query to each address in
supplied range and lists received information in human
readable form. For each responded host it lists IP address,
NetBIOS computer name, logged-in user name and MAC address 
(such as Ethernet).

See http://www.inetcat.org/software/nbtscan.html for
NBTscan homepage.

## LICENSE.

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program (in a file called COPYING); if not, write 
to the Free Software Foundation, Inc., 675 Mass Ave, Cambridge, 
MA 02139, USA.

## INSTALLATION.

NBTscan compiles and runs on Unix and Windows. I have tested it
on Windows NT 4.0, Windows 2000, FreeBSD 4.3, OpenBSD 2.8
and RedHat Linux 7.1. It should also compile and run on Solaris
and other Linuxes as well.  Steve Coleman 
<Steve.Coleman@jhuapl.edu> ported NBTscan to Solaris, HP-UX and 
OSF/1 and fixed several bugs. He reports that NBTscan also runs 
on IRIX/SGI with minor problems. Mohammad A. Haque 
<mhaque@haque.net> ported nbtscan to Darwin.

### Windows:

To compile this under Windows you will need Cygwin. You can
Download and install Cygwin from 
http://sources.redhat.com/cygwin/
Start Cygwin shell and proceed from there as in Unix 
installation

### Unix

```
./configure

make

make install
```

That's all.

## RUNNING.

Usage:

```
nbtscan [-v] [-d] [-e] [-l] [-t timeout] [-b bandwidth] [-r] [-q] [-s separator] [-m retransmits] (-f filename)|(<scan_range>) 
        -v              verbose output. Print all names received
                        from each host
        -d              dump packets. Print whole packet contents.
        -e              Format output in /etc/hosts format.
        -l              Format output in lmhosts format.
                        Cannot be used with -v, -s or -h options.
        -t timeout      wait timeout imilliseconds for response.
                        Default 1.
        -b bandwidth    Output throttling. Slow down output
                        so that it uses no more that bandwidth bps.
                        Useful on slow links, so that ougoing queries
                        don't get dropped.
        -r              use local port 137 for scans. Win95 boxes
                        respond to this only.
                        You need to be root to use this option on Unix.
        -q              Suppress banners and error messages,
        -s separator    Script-friendly output. Don't print
                        column and record headers, separate fields 
			with separator.
        -h              Print human-readable names for services.

                        Can only be used with -v option.
        -m retransmits  Number of retransmits. Default 0.
        -f filename     Take IP addresses to scan from file filename
			-f - makes nbtscan take IP addresses from stdin.
        <scan_range>    what to scan. Can either be single IP
                        like 192.168.1.1 or
                        range of addresses in one of two forms: 
                        xxx.xxx.xxx.xxx/xx or xxx.xxx.xxx.xxx-xxx.
```

Examples:

```
nbtscan -r 192.168.1.0/24
```

Scans the whole C-class network.

```
nbtscan 192.168.1.25-137
```

Scans a range from 192.168.1.25 to 192.168.1.137

```
nbtscan -v -s : 192.168.1.0/24
```

Scans C-class network. Prints results in script-friendly
format using colon as field separator.
Produces output like that:

```
192.168.0.1:NT_SERVER:00U
192.168.0.1:MY_DOMAIN:00G
192.168.0.1:ADMINISTRATOR:03U
192.168.0.2:OTHER_BOX:00U
...
```

```
nbtscan -f iplist
```

Scans IP addresses specified in file iplist.

## BUGS/LIMITATIONS

Windows version has a certain limitation: you cannot scan Win95 
hosts with it because Windows 95 always sends responses to name 
queries to port 137, and you cannot bind to port 137 under
Windows (it is already taken by Windows itself).

When talking to Samba boxes nbtscan always reports the MAC 
address being 00-00-00-00-00-00. This is because Samba sends 
that as MAC address. Nbtscan just displays what it gets.

Report bugs to alla@inetcat.org (that's me). I cannot promise to
do anything but I might well want fix it. Remember: no warranty.
