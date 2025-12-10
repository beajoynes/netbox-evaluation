
## Useful sites
* Ansible Galaxy collection https://galaxy.ansible.com/ui/repo/published/netbox/netbox/
* Netbox namespace collections (Netbox.Netbox) - community docs
* - Netbox **inventory** source https://docs.ansible.com/projects/ansible/latest/collections/netbox/netbox/nb_inventory_inventory.html
  - Netbox **lookup** https://docs.ansible.com/projects/ansible/latest/collections/netbox/netbox/nb_lookup_lookup.html
* **Semaphore** ansible tasks docs https://docs.semaphoreui.com/user-guide/task-templates/apps/ansible/
* Ansible cheat sheet https://www.geeksforgeeks.org/devops/ansible-cheat-sheet/

  
## Install

`ansible-galaxy collection install netbox.netbox`

To check it is installed run `ansible-galaxy collection list | grep netbox` :
```
netbox.netbox                            3.21.0
```
## Environment variables

### Add temporary environment variables for the current shell session using : 
```
export NETBOX_API=http://172.28.227.204:8000/
export NETBOX_TOKEN=6359cf4bd054e0a0c59fbedc316f938909b18260
```

Storing the netbox URL and API token as environment variables is a secure method as you then don't have sensitive information in the playbooks themselves, they can be referenced using `"{{ lookup('env', 'NETBOX_API') }}"` and `"{{ lookup('env', 'NETBOX_TOKEN') }}"` respectively.

Use `printenv | grep NETBOX` to check if the correct variables are stored.

### Permanently adding to the virtual environment’s activate script
This ensures variables are set only when the venv is active.

Open the activate script:
```
nano path/to/venv/bin/activate
```
Add your variables at the end:
```
export SECRET_KEY="mysecret"
export DEBUG="True"
```
Save and reactivate:
```
source path/to/venv/bin/activate
```

> [Ansible vault](https://docs.ansible.com/projects/ansible/latest/vault_guide/vault.html) can also be used to keep sensitive information hidden and secure. 

## Example : Basic playbook
`nano basic_playbook.yml`

Creating a playbook (YAML file) to create two manufacturers, using the netbox.netbox_
```
- name: "Basic Playbook"
  connection: local
  hosts: localhost
  gather_facts: False


  tasks:
    - name: Create Juniper Manufacturer
      netbox.netbox.netbox_manufacturer:
        netbox_url: "{{ lookup('env', 'NETBOX_API') }}"
        netbox_token: "{{ lookup('env', 'NETBOX_TOKEN') }}"
        data:
          name: Juniper
        state: present
    - name: Create Disco Manufacturer
      netbox.netbox.netbox_manufacturer:
        netbox_url: "{{ lookup('env', 'NETBOX_API') }}"
        netbox_token: "{{ lookup('env', 'NETBOX_TOKEN') }}"
        data:
          name: Disco
        state: present
```

I get the following output :
```
PLAY [Basic Playbook] **********************************************************

TASK [Create Juniper Manufacturer] *********************************************
ok: [localhost]

TASK [Create Disco Manufacturer] ***********************************************
changed: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

It shows that both tasks were completed successfully, but only the second one changed anything - this is expected as Juniper already exists as a manufacturer while Disco is new and was added to the database.

Navigating to `http://172.28.227.204:8000/dcim/manufacturers/` and I can see the Disco manufacturer is now there.
