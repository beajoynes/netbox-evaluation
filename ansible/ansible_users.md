"Local connection" in AWX Kubernetes = AWX pod's local filesystem, NOT your WSL machine. The AWX pod has:

```text
❌ No Docker daemon
❌ No Docker socket (/var/run/docker.sock)  
❌ No containerlab binary
❌ No /usr/local/bin
❌ Minimal Alpine Linux base (no docker client)
❌ No network access to your WSL Docker
```
### The Solution: SSH Connection (Not Local)
Change your inventory from local → SSH to WSL:

```
all:
  hosts:
    clab_host:
      ansible_host: 192.168.0.183      # Your WSL IP
      ansible_user: beaj               # Your WSL user
      ansible_ssh_private_key_file: "~/.ssh/id_ed25519"  # Your key
      ansible_python_interpreter: /usr/bin/python3
```
### AWX Job Template Settings
```text
✅ Inventory: SSH inventory (above)
✅ Privilege Escalation: OFF  (beaj in docker group)
✅ Execution Environment: default awx-ee
✅ Playbook: /tmp/containerlab version (works anywhere)
```
### Why This Works Perfectly
```text
AWX Pod ──SSH──→ WSL (192.168.0.183)
  ↓                 ↓
[isolated]      [docker, containerlab, /home/beaj]
  │               ✓ Full environment
  └─runs playbook → ✓ Docker access
                     ✓ containerlab binary  
                     ✓ /home/beaj writable
```
