# Changelog

All notable changes to this project are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [0.3.9] - 2026-10-04

### Added
- `-t backup` collection type, and NetBackup collection is now part of `all`; it was previously never called

### Fixed
- NetBackup tools are looked up in `bin`, `bin/admincmd` and `/usr/openv/volmgr/bin` rather than the top-level netbackup directory

## [0.3.8] - 2026-10-04

### Fixed
- `kernel_info` was never called. It now runs as part of `hardware` (and so `all`), collecting sysctl, uname, runlevel, slabtop, module and kernel config details
- Skip kernel tools that are not installed and create the output directories `kernel_info` needs

## [0.3.7] - 2026-10-04

### Changed
- Use `$((Mem / 1000000))` instead of a useless `echo $(( ))`
- Group the `cpu_details.txt` redirects into one block
- Replace `ls | grep` in the device-mapper lookup with `ls | awk`

## [0.3.6] - 2026-10-04

### Removed
- Leftover `DEBUG: TOPDIR` message printed with `-d`

## [0.3.5] - 2026-10-04

### Added
- `CopyTree` helper that uses rsync when present and falls back to `cp -a`

### Fixed
- `/etc` and `/var/log` were not collected on systems without rsync

## [0.3.4] - 2026-10-04

### Changed
- `mywhich` uses the `type -P` builtin instead of the external `which`

## [0.3.3] - 2026-10-04

### Fixed
- `cpu_details.txt` reported the core count as the processor count, and now reports the number of processors
- `/proc/filesystem` typo (now `/proc/filesystems`)
- Stray `sysctl` argument in the Mac OS X `machdep.cpu.thread_count` query

## [0.3.2] - 2026-10-04

### Fixed
- `EXIMTOPTDIR` and `DOVETOPTDIR` typos made `MakeDir` fail with an empty path and abort the run whenever exim or dovecot was installed

## [0.3.1] - 2026-10-04

### Changed
- Test command success directly (`if ! cmd`) instead of checking `$?` afterwards

## [0.3.0] - 2026-10-04

### Changed
- `read` uses `-r` so backslashes are not mangled
- Backticks replaced with `$(...)`
- `egrep` replaced with `grep -E`
- Removed needless escapes in the `fc_host` glob and the dmidecode `awk` separator, and a misplaced quote in a `sed` expression

## [0.2.9] - 2026-10-04

### Fixed
- Quote variable expansions throughout the script so paths and values with spaces or glob characters are handled safely
- `[ -x $VAR ]` tests were always true when the variable was unset, creating empty ioreg and system_profiler output files on Linux

## [0.2.8] - 2026-10-04

### Removed
- Unused command lookups from `findCmds` (`basename`, `cut`, `file`, `gpg`, `egrep`, `ln`, `locale`, `sleep`, `mv`, `sar`, `tail`, `zip`, `gzip`, `gawk`, `apt-config`, `emerge`, `lspnp`, `ipvsadm`, `debugreiserfs`, `pvs` duplicate, `vxlicrep`, `iostat`, `xvinfo`, and the misspelled `HWPARM` duplicate of `HDPARM`)

## [0.2.7] - 2026-10-04

### Fixed
- `mywhich` declares and assigns `mypath` separately so the `which` exit status is not masked

## [0.2.6] - 2026-10-04

### Changed
- `btrfs fi show` is now `btrfs filesystem show`, and its output file is renamed to `btrfs_filesystem_show.out`

## [0.2.5] - 2026-10-04

### Fixed
- Quote grep patterns in the device-mapper and bridge collectors so the shell cannot glob them

## [0.2.4] - 2026-10-04

### Fixed
- Quote the kernel release in the `modules.dep` copy path

## [0.2.3] - 2026-10-04

### Fixed
- Check that `cd $TOPDIR` succeeds before creating the tarball

## [0.2.2] - 2026-10-04

### Fixed
- Date stamp used the month twice (`%m`) instead of a single `%Y.%m.%d.%H.%M`

## [0.2.1] - 2026-10-04

### Fixed
- Typo in bridge output filenames (`btctl_*` is now `brctl_*`)

## [0.2.0] - 2026-10-04

### Fixed
- `mywhich` no longer echoes the bare command name for missing tools; it returns `NOT_FOUND` consistently

## [0.1.9] - 2026-10-04

### Fixed
- `copy_etc` now also removes `gshadow`, backup shadow files, `security/opasswd` and SSH host private keys from the copy

## [0.1.8] - 2026-10-04

### Fixed
- EMC PowerPath device loop no longer errors when no `/dev/emcpower*` devices exist

## [0.1.7] - 2026-10-04

### Fixed
- WWID mapping used an unset `disk_short` variable, leaving the disk name blank
- SCSI disk loop listed `[a-z]d[a-z]` relative to the current directory instead of `/dev`

## [0.1.6] - 2026-10-04

### Fixed
- NetBackup collection ran only when NetBackup was not installed
- `$NBackupDir` typo wrote configs to `/configs`

## [0.1.5] - 2026-10-04

### Fixed
- `-t cluster` and `-t clusters` both select the cluster section
- `-t general` printed the wrong section name
- Usage text lists the valid `-t` values

## [0.1.4] - 2026-10-04

### Fixed
- Stop deleting the whole target directory at startup, which removed earlier runs and anything else in `-d`

## [0.1.3] - 2026-10-04

### Fixed
- Invalid options and missing option arguments now print an error and usage instead of being ignored

## [0.1.2] - 2026-10-04

### Fixed
- `-k` no longer consumes the next argument
- `-s` and `-D` are now accepted by option parsing

## [0.1.1] - 2026-10-04

### Fixed
- `-k` removed the collected files instead of keeping them (inverted check)
- Script version variable now matches the changelog

## [0.1.0] - 2022-01-31

### Fixed
- Fixes for cp/rsync and dovecot from Mark Lane

## [0.0.9] - 2016-10-10

### Fixed
- Fixed hostid on Mac OS X

## [0.0.8] - 2016-10-10

### Changed
- Substituted ioreg for lspci on OS X and added system_profiler output

## [0.0.7] - 2016-10-10

### Added
- Very basic Mac OS X support

## [0.0.6] - 2016-10-10

### Changed
- Cleaned up uname and hostid

## [0.0.5] - 2016-10-10

### Changed
- Directed software output to patch+pkg directory like STB

## [0.0.4] - 2016-10-09

### Changed
- Directed hardware, disk and system output to locations similar to STB

## [0.0.3] - 2016-10-09

### Changed
- Started updating behavior to be more like recent versions of explorer (STB)

## [0.0.2] - 2016-10-08

### Changed
- Initial code cleanup

## [0.0.1] - 2016-10-08

### Added
- Initial import
