# User and Group Commands
## Modifying Users
Part of the "Shadow Password Suite" used to manage user accounts
`useradd`= Create new user account or update existing account
`id` = Show user and group ID for all possible ones
`id username` = Show uid and gid for `username`

`userdel` = Deletes user account 
`userdel -r` = Deletes user account + their home directory

`usermod` = Modify user information (home dir, shell, UID, GID, etc.). Can be used on list of usernames
`usermod -aG groupname username` = Add user to a group
`usermod -d /path/to/new/homedir` = Change user's home dir
`usermod -L username` = Lock/unlock user (password hash hidden)
`usermod -u UID -g GID username` = Changes UID and GID of user

## Files, Directories, Permissions
`chmod` = Changes permission of file/directory. Use `-R` for recursive inside directory.
`chown` = Changes owner and group of file/directory. Also use `-R` for recursive inside directory. e.g. `sudo chown -R username:group /path/to/folder`
`chgrp` = Changes group of file/directory. Also can use `-R` for recursive

## Modifying Groups
Groups are used to organize users and define access privilege to files & directories.
`groupadd` = Create new group.
`groupmod` = Modifies group properties
`groupmod -n oldname newname` = Changes group name
`grpck` = Check integrity of group files on system (Checks if have valid password files I think??)
`groupdel` = Deletes group. Use `-f` to force delete, along with any users inside that group.

## Password Management
#Note All these `chk` commands checks for integrity and consistency between files. e.g. checking if user account exists in `passwd` file but not in `shadow` file due to manual edit.

`pwck` = Checks for password file inconsistencies and integrity
Use `vipw` and `vigr` to manually change `/etc/passwd` and `/etc/shadow` to solve integrity issues

`chage` = Change aging and expiration policy of user's password. Used to enforce password policy for security hardening. (e.g. time between pass changes, max number of tries, etc.)
`chage -l username` = Shows password aging info for user
`chage -d username` = Sets date of last password change for user
`chage -E username` = Sets date of password expiry for user

`passwd` = Manage user passwords. (Own or others as sudo)
#Note edit `/etc/security/pwquality.conf` to configure password policy settings
`passwd username` = Changes password for user
`passwd -l username` = Locks password for user (??)
`password -u user` = Unlocks password for user

## Locating Files
`find` = Search for files and directories based on criteria
e.g. `find . -name "*.txt"`

`locate` = Uses pre-built database to search for files based on name/pattern (Faster than find since uses pre-made data set)
e.g. `locate sensitive`

`whereis` = Finds binary, source, manual pages for a given command.
e.g. `whereis ls` Gives binary, source, manual page location for `ls` command
