Mount everything inside /run as nosuid,noexec,nodev,noatime
Remove all SUID in /usr and mount it as nosuid,nodev

nosuid = All Directories
noexec = Except /usr, /etc, /var/lib/flatpak
nodev = Except /sys/fs/selinux, /dev, /dev/pts
