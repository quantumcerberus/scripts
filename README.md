Mount everything inside /run as nosuid,noexec,nodev,noatime
Remove all SUID in /usr and mount it as nosuid,nodev

Ideal:
suid = nothing
exec = /usr, /etc, /var/lib/flatpak
dev = /sys/fs/selinux, /dev, /dev/pts
