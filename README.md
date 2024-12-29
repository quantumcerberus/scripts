- Automount everything inside /run as nosuid,noexec,nodev
- Remove all SUID in /usr and mount it as nosuid,nodev

- Ideal:
- suid = nothing
- exec = /usr, /etc, /var/lib/flatpak
- dev = /dev, /dev/pts, /sys/fs/selinux

module block_run_exec 1.0;

require {
    type tmp_t;
    type run_t;
    class file { execute execute_no_trans };
    class dir { add_name remove_name search };
}

# Deny execution on files inside /run
# This rule will block anything from executing inside the /run directory
deny run_t:file { execute execute_no_trans };

checkmodule -M -m -o block_run_exec.mod block_run_exec.te
semodule_package -o block_run_exec.pp -m block_run_exec.mod
semodule -i block_run_exec.pp

semanage fcontext -l | grep '/run'
