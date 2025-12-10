[Inventory docs](https://docs.ansible.com/projects/ansible/latest/inventory_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups)


# Use host variables to define 'connection variables'
Enables task execution on the host by configuring `connection`, `shell`, and `become` plugins.
```
[targets]

localhost              ansible_connection=local
other1.example.com     ansible_connection=ssh        ansible_user=myuser
other2.example.com     ansible_connection=ssh        ansible_user=myotheruser
```
## Connection plugins 
Run `ansible-doc -t connection -l`

```
amazon.aws.aws_ssm                   connect to EC2 instances via AWS Systems Manager
ansible.builtin.local                execute on controller
ansible.builtin.paramiko_ssh         Run tasks via Python SSH (paramiko)
ansible.builtin.psrp                 Run tasks over Microsoft PowerShell Remoting Protocol
ansible.builtin.ssh                  connect via SSH client binary
ansible.builtin.winrm                Run tasks over Microsoft's WinRM
ansible.netcommon.grpc               Provides a persistent connection using the gRPC protocol
ansible.netcommon.httpapi            Use httpapi to run command on network appliances
ansible.netcommon.libssh             Run tasks using libssh for ssh connection
ansible.netcommon.netconf            Provides a persistent connection using the netconf protocol
ansible.netcommon.network_cli        Use network_cli to run command on network appliances
ansible.netcommon.persistent         Use a persistent unix socket for connection
community.docker.docker              Run tasks in docker containers
community.docker.docker_api          Run tasks in docker containers
community.docker.nsenter             execute on host running controller container
community.general.chroot             Interact with local chroot
community.general.funcd              Use funcd to connect to target
community.general.incus              Run tasks in Incus instances using the Incus CLI
community.general.iocage             Run tasks in iocage jails
community.general.jail               Run tasks in jails
community.general.lxc                Run tasks in LXC containers using lxc python library
community.general.lxd                Run tasks in LXD instances using `lxc' CLI
community.general.qubes              Interact with an existing QubesOS AppVM
community.general.saltstack          Allow ansible to piggyback on salt minions
community.general.wsl                Run tasks in WSL distribution using wsl.exe CLI using SSH
community.general.zone               Run tasks in a zone instance
:...skipping...
amazon.aws.aws_ssm                   connect to EC2 instances via AWS Systems >
ansible.builtin.local                execute on controller                    >
ansible.builtin.paramiko_ssh         Run tasks via Python SSH (paramiko)      >
ansible.builtin.psrp                 Run tasks over Microsoft PowerShell Remot>
ansible.builtin.ssh                  connect via SSH client binary            >
ansible.builtin.winrm                Run tasks over Microsoft's WinRM         >
ansible.netcommon.grpc               Provides a persistent connection using th>
ansible.netcommon.httpapi            Use httpapi to run command on network app>
ansible.netcommon.libssh             Run tasks using libssh for ssh connection>
ansible.netcommon.netconf            Provides a persistent connection using th>
ansible.netcommon.network_cli        Use network_cli to run command on network>
ansible.netcommon.persistent         Use a persistent unix socket for connecti>
community.docker.docker              Run tasks in docker containers           >
community.docker.docker_api          Run tasks in docker containers           >
community.docker.nsenter             execute on host running controller contai>
community.general.chroot             Interact with local chroot               >
community.general.funcd              Use funcd to connect to target           >
community.general.incus              Run tasks in Incus instances using the In>
community.general.iocage             Run tasks in iocage jails                >
community.general.jail               Run tasks in jails                       >
community.general.lxc                Run tasks in LXC containers using lxc pyt>
community.general.lxd                Run tasks in LXD instances using `lxc' CL>
community.general.qubes              Interact with an existing QubesOS AppVM  >
community.general.saltstack          Allow ansible to piggyback on salt minion>
community.general.wsl                Run tasks in WSL distribution using wsl.e>
community.general.zone               Run tasks in a zone instance             >
community.libvirt.libvirt_lxc        Run tasks in lxc containers via libvirt  >
community.libvirt.libvirt_qemu       Run tasks on libvirt/qemu virtual machine>
community.okd.oc                     Execute tasks in pods running on OpenShif>
community.proxmox.proxmox_pct_remote Run tasks in Proxmox LXC container instan>
community.vmware.vmware_tools        Execute tasks inside a VM via VMware Tool>
containers.podman.buildah            Interact with an existing buildah contain>
containers.podman.podman             Interact with an existing podman containe>
google.cloud.iap                     connect via SSH through Google Cloud's Id>
kubernetes.core.kubectl              Execute tasks in pods running on Kubernet>
```

Tried `ansible-doc -t connection community.docker.docker` but got this :
```
[WARNING]: community.docker.docker was not found
```
