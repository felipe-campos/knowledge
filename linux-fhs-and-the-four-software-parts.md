## Linux Directory Hierarchy: Oriented to the [Four Software Parts](software-parts.md)

from [The Linux Documentation Project](http://www.tldp.org/HOWTO/HighQuality-Apps-HOWTO/fhs.html) (with little modification).

see also

- [_Linux Directory Map_ post by d4nyll](http://blog.danyll.com/linux-directory-map/)
- [FHS 3.0](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html)
- [FHS 2.3](http://www.pathname.com/fhs/)

On Linux, the [Four Software Parts](software-parts.md) theory is expressed in its directory structure, which is classified and documented in the [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/). FHS is part of the [LSB (Linux Standar Base)](http://www.linuxbase.org/). It defines in which directories each piece of Apache, Samba, Mozilla, KDE _and your Software_ must go.

### 1. FHS Summary

Directory | Description
----------|------------
`/usr/bin` | Directory for the executables accessed by all users (everybody have this directory in their `$PATH`). The main files of your Software will probably be here. **You should never create a subdirectory under this folder**.
`/bin` | Like `/usr/bin`, but here you’ll find only boot process vital executables, which are simple and small. Your software (being high-level) probably doesn’t have anything to install here.
`/usr/sbin` | Like `/usr/bin`, but contains only the executables that must be accessed by the administrator (root user). Regular users should never have this directory in their `$PATH`. If your software is a daemon, this is the directory for some of the executables.
`/sbin` | Like `/usr/sbin`, but only for the boot process vital executables that will be accessed by sysadmin for some system maintaining. Commands like `fsck` (filesystem check), `init` (father of all processes), `ifconfig` (network configuration), `mount` etc. can be found here. It is the system’s most vital directory.
`/usr/lib` | Contains dynamic libraries and support static files for the executables at `/usr/bin` and `/usr/sbin`. You can create a subdirectory like `/usr/lib/myproduct` to contain your helper files, or dynamic libraries that will be accessed only by your Software, without user intervention. A subdirectory here can be used as a container for plugins and extensions.
`/lib` | Like `/usr/lib` but contains dynamic libraries and support static files needed in the boot process. You’ll never find an executable at `/bin` or `/sbin` that needs a library that is outside this directory. Kernel modules (device drivers) are under `/lib`.
`/etc` | Contains configuration files. If your Software uses several files, put them under a subfolder like `/etc/myproduct`.
`/var` | The name comes from _‘variable’_. Everything in this directory changes frequently and the package system (RPM) doesn’t keep control of it. Usually `/var` is mounted over a separate high-performance partition. In `/var/log` logfiles grow up. For web content we use `/var/www`.
`/home` | Contains the user’s (real human beings) _home_ directories. **Your Software package should never install files here (in installation time)**. If your business logic requires a special UNIX user (not a human being) to be created, you should assign him a home directory under `/var` or other place outside `/home`. Please, never forget that.
`/usr/share/doc`, `/usr/share/man` | The _‘share’_ word is used because what is under `/usr/share` is platform independent and can be shared among several machines across a network filesystem. Therefore, this is the place for manuals, documentations, examples etc.
`/usr/local`, `/opt` | Obsolete folders. When UNIX didn’t have a package system (like RPM), sysadmins needed to separate an _optional_ (or _local_) Software from the main OS. These were the directories used for that.

### 2. Examples Using the FHS

| Software on its Own | Configurations | Content | Logs, Dumps etc.
----------------------|----------------|---------|-----------------
**Database Server** | `/usr/bin/`, `/usr/lib/`, `/usr/share/doc/mydb/`, `/usr/share/doc/mydb/examples/` | `/etc/mydb/` | `/var/db/instance1/`, `/var/db/instance2/` etc. | `/var/db/instance1/transactions/`, `/var/log/db/access-instance1.log`, `/var/log/db/access-instance2.log`
**Text Editor** | `/usr/bin/`, `/usr/lib/`, `/usr/lib/myeditor/plugins/`, `/usr/share/myeditor/templates`, `/usr/share/doc/myeditor/` | `$HOME/.myeditor.conf` | `$HOME/Docs/` | `$HOME/.myeditor-tmp/`
**MP3 Generator** | `/usr/bin/`, `/usr/lib/`, `/usr/lib/mymp3/plugins/`, `/usr/share/doc/mymp3/` | `$HOME/.mymp3.conf` | `$HOME/Music/` | `$HOME/.mymp3-tmp/`
**Web Server** | `/usr/sbin/`, `/usr/bin/`, `/usr/lib/httpd-modules/`,`/usr/share/doc/httpd/`, `/usr/share/doc/httpd/examples/` | `/etc/httpd/`, `/etc/httpd/instance1/`, `/etc/httpd/instance2/` | `/var/www/`, `/var/www/instance1/`, `/var/www/instance2/` | `/var/logs/httpd/`, `/var/logs/httpd/instance1/`, `/var/logs/httpd/instance2/`
**E-Mail Server** | `/usr/sbin/`, `/usr/bin/`, `/usr/lib/`, `/usr/share/doc/myemail/` | `/etc/mail/`, `/etc/mailserver.cf` | `/var/mail/` | `/var/spool/mailqueue/`, `/var/logs/mail.log`

### 3. Linux Directory Roadmap by d4nyll

![alt text](http://blog.danyll.com/content/images/2015/04/linux_directory_map_hd.png "FHS Roadmap")

### 4. Good StackOverflow Answers About FHS
---

[link to original thread](http://askubuntu.com/questions/308045/differences-between-bin-sbin-usr-bin-usr-sbin-usr-local-bin-usr-local)


-  `/bin` : For binaries usable before the `/usr` partition is mounted. This is used for trivial binaries used in the very early boot stage or ones that you need to have available in booting single-user mode. Think of binaries like `cat`, `ls`, etc.

-  `/sbin`  : Same, but for scripts with *superuser (root) privileges required*.

- `/usr/bin` : Same as first, but for *general system-wide binaries*.

- `/usr/sbin` : Same as above, but for scripts with superuser (root) privileges required.

> if I'm writing my own scripts, where should I add these?

None of the above. You should use `/usr/local/bin` or `/usr/local/sbin` for system-wide available scripts. The `local` path means it's not managed by the system packages (this is [an error](http://lintian.debian.org/tags/file-in-usr-local.html) for Debian/Ubuntu packages).

For *user-scoped scripts*, use `~/bin` (a personal bin folder in your home directory).

The FHS says for `/usr/local`:

> Tertiary hierarchy for local data, *specific to this host*. Typically has further subdirectories, e.g., `bin/`, `lib/`, `share/`.

---

[link to original thread](http://askubuntu.com/questions/138547/how-to-understand-the-ubuntu-file-system-layout)

Basically Linux has divided the directory structure based on the function of what is needed to make the system as secure as possible with the minimum amount of permissions needed. Otherwise someone is bound to have to do a lot of avoidable work.

Remember that Unix and Linux where made as multi-user systems and Windows was created for a single user. Everything else can be explained from that idea. You can explain every directory when thinking about it being multi-user and security.

3 examples:

- You will see that files and directories that are admin only are gathered in the same directory: the s in `/sbin` and `/usr/sbin` and `/usr/local/sbin` stands for system. A normal user can not even start programs that are in there. Files a normal user can start are in /bin, /usr/bin, /usr/local/bin based on where it most logically should reside. But if they are admin only they should go to the `s` version of that directory.
There is a famous utility called `fuser`. You can kill processes with it. If a normal user could use this (s)he would be able to kill your session.

- The same goes for `/home`: /home/user1 is property of user1. /home/user2 is property of user2. user2 has no business doing stuff in user1's home (and the other way around is also true: user1 has no business doing stuff in user2's home). If all the files would be in /home with no username underneath it you would have to give permissions to every file and asses if someone is allowed to write/remove those files. A nightmare if you have tens of users.

- Addition regarding libraries.

  `/lib/`, `/usr/lib/`, and `/usr/local/lib/` are the original locations, from before multilib
systems existed and the exist to prevent breaking things. `/usr/lib32`, `/usr/lib/64`, `/usr/local/lib32/`, `/usr/local/lib64/` are 32-/64-bit multilib inventions.


It is not a static concept by any means. Other Linux flavours made tweaks to this lay-out. For instance; currently you will see [debian and Ubuntu](http://wiki.debian.org/ReleaseGoals/RunDirectory#A.2BAC8-run) changing a lot in the lay-out of the FHS since SSD is better off with read only files. There is a movement towards a new lay-out where files are split in to a 'read only' and a 'writable' directory/group so we can have a root partition that can be mounted read only (partition for a ssd) and writable (sata hdd).
The new directory that is used for this (not in the image) is `/run/`.

### 5. `$ man hier`

`$ man hier`
