![alt tag](https://raw.githubusercontent.com/lateralblast/LINUXexplo/master/explorer.jpg)

LINUXexplo
==========

A version of SUNWexplo (now called STB) for Linux.

Introduction
------------

This expands on and modernises the great work done J.S. Unix Consultants Ltd:

http://www.unix-consultants.co.uk/examples/scripts/linux/linux-explorer/

What it does
------------

`explorer` is a single Bash script that gathers configuration and diagnostic
information about a system and bundles it into a compressed tar file that can
be sent to a support team. Output is laid out like STB/SUNWexplo (`disks`,
`patch+pkg`, `sysconfig` and so on) so existing tooling and habits carry over.

Information is collected only where the relevant tool or file is present, so
the same script runs across different distributions. Tool locations are looked
up at run time rather than assumed.

Requirements
------------

- Bash
- Root access (the script exits if it is not run as root)
- Standard utilities such as `tar`, `awk`, `sed`, `grep` and `md5sum`
- `rsync` is used to copy `/etc` and `/var/log` if available, otherwise `cp -a`
- Linux. Mac OS X has very basic, experimental support

Usage
-----

Run as root:

    ./explorer [options]

Options:

| Option | Description |
|--------|-------------|
| `-d <dir>` | Directory to write output to (default `/var/explorer/output`) |
| `-t <type>` | Only collect one section (see below). Default is `all` |
| `-k` | Keep the uncompressed output directory as well as the tar file |
| `-v` | Verbose output showing progress |
| `-s` | Verify package installation (very slow) |
| `-g` | Create explorer config |
| `-V` | Show version |
| `-h` | Show help |

Examples:

    # Collect everything into the default location
    sudo ./explorer

    # Collect only disk information into /tmp/out, keep the raw files, be verbose
    sudo ./explorer -v -k -d /tmp/out -t disks

Collection types
----------------

| Type | Contents |
|------|----------|
| `configs` | Boot loader configuration and boot services |
| `clusters` | Red Hat Cluster, Veritas Cluster and Pacemaker details |
| `disks` | Disks, partitions, Btrfs, LVM, ZFS, filesystems, RAID, device mapper, NFS, EMC PowerPath, NetApp and Veritas Volume Manager |
| `hardware` | Hardware, CPU, memory and PCI details, plus `disks` and `network` |
| `logs` | System logs, SELinux and `/proc` and `/sys` information |
| `network` | Interfaces, iptables, ipchains, ethtool and NIS (YP) |
| `software` | RPM, DEB, pacman, zypper, Gentoo, Spacewalk/RHN, Samba and Apache |
| `virtualization` | Xen, libvirt and Docker |
| `general` | Printing, mail (Postfix, Exim, Dovecot), time, X11, Apache, Samba and system logs |
| `all` | All of the above (default) |

Regardless of type, the script always copies `/etc` (leaving out password
hashes and SSH host keys), records systemd status, performance statistics and
installation details, and writes the script version to a `rev` file.

Output
------

Each run creates `explorer.<hostid>.<hostname>-<date>` under the output
directory and packs it into `explorer.<hostid>.<hostname>-<date>.tar.gz`. When
run from a terminal the script prints the tar file name and its MD5 sum. Send
both to your support representative.

Inside the tree, output files are named after the command that produced them
(for example `disks/fdisk_-l_sda.out`). Common directories are `boot`,
`disks`, `etc`, `logs`, `mail`, `networks`, `patch+pkg`, `sysconfig`,
`system`, `var` and `virtual`. Commands that could not be found are listed in
`command_not_found.out`.

Version
-------

Current version: **0.3.7** (see [CHANGELOG.md](CHANGELOG.md))

Help Support Development
------------------------

If you find this software useful and would like to support its development, please consider buying me a coffee:

https://ko-fi.com/richardatlateralblast

License
-------

Licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). See [LICENSE](LICENSE).
