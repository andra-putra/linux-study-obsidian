# File Compression and Archival

## Gunzip and Gzip
Deals with `.gz` files. Compresses singular files.

`gzip` = "GNU Zip". Just do `gzip file` to use.
`gunzip` = "GNU Unzip". Just do `gunzip file.gz` to use.

## tar, rar, unrar
#### tar
Deals with `.tar` files. Archives entire directories into one file, then use `gzip` to compress them. Often see it as `.tar.gz` which means its combined into one big file, which is then compressed.
#funfact`tar` stands for "Tape Archive"

`tar [options] [archive-file] [file or directory to be archived]` = tar usage
e.g. `tar -cvzf webBackups.tar.gz webBackups/` = Backs up entire `webBackups/` directory into a file named `webBackups.tar.gaz` using `gzip` algorithm
Common options:
`tar -tf filename.tar.gz` = Views, but not extract files from tar archive
`tar -xf filename.tar.gz` = Extracts files from tar archive

| Option | Meaning                          |
| ------ | -------------------------------- |
| c      | create new archive               |
| v      | Display progress info (verbose)  |
| z      | Use gzip algorithm               |
| f      | Specify output archive file name |
#### rar, unrar
Deals with `.rar` files
Basically combines `.gz` and `.tar`.
Can use password protection, error recovery, split large files into multiple smaller ones, etc.
#note Does not come with Fedora. Must do `dnf install unrar`. Can't do rar though for some reason. Will have to come back to this in the future.

#### Zip, Unzip
Deals with `.zip` files.
Basically combines `.gz` and `.tar`.

e.g. 
`zip -r backup.zip web_server/` = Recursively zips `web_server/` directory to file named `backup.zip`
`unzip backup.zip -d new_web_server/` = Unzips `backup.zip` into new dir named `new_web_server/`

#### bunzip2, bzip2, etc.
Deals with `.bz2` files.
Used mostly on unix based systems. Ideal for compressing large files and directories.

e.g.
`bzip2 -k -v logfile.log` = Makes compressed version of specified file. `-k` Keeps original file too, while `-v` displays verbose progress.
`tar -cvf - logfiles/ | bzip2 -9 -c > logfiles.tar.bz2` = Creates tar archive of `logfiles`, then compresses it with maximum `-9` compression, then redirects output to backup file `logfiles.tar.bz2`
- `-` in `tar` command means it should send the command output to `stdout`, hence can `|` pipe it
- `-9` in `bzip2` is the max level of compression. Can do from `-1` to `-9`
- `-c` in `bzip2` sends command output to `stdout`, hence can redirect using `>`to `logfiles.tar.bz2`

`bunzip2` = Decompress `.bz2` and even `.gz` files
e.g.
`bunzip2 file.bz2` 
`cat syslog.log.bz2 | bunzip2 -c > syslog.log` = Can be used to combine split apart files by using `cat` to concatenate into `stdout`, then piping it to `bunzip2`


#### 7zip
Can handle `.zip`, `.gz`, `.tar`, `.7z` formats.
More secure compression method apparently.
#note on Fedora needs to install using `dnf install p7zip p7zip-plugins`

e.g.
`7z a -t7z -p -mhe=on archive.7z dir/to/compress/` = Makes password protected and encrypted `.7z` archive.
- `-mhe=on` Enables encryption of filenames
- `-p` Enables password for compressed archive
- `-t7z` Makes a `.7z` archive file

#### XZ
Deals with `.xz` files.
High compression ratio and low memory usage.
Used for compressing Linux kernel during installs.

e.g.
`xz -z -k -9 syslog.log`
- `-9` Maximum compression level
- `-k` Keeps original file
`xz -d logfile.log.xz`
- `-d` Decompress file
