
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
### Environment variables

```
export NETBOX_API=http://172.28.227.204:8000/
export NETBOX_TOKEN=6359cf4bd054e0a0c59fbedc316f938909b18260
```

Storing the netbox URL and API token as environment variables is a secure method as you then don't have sensitive information in the playbooks themselves, they can be referenced using `"{{ lookup('env', 'NETBOX_API') }}"` and `"{{ lookup('env', 'NETBOX_TOKEN') }}"` respectively.

> [Ansible vault](https://docs.ansible.com/projects/ansible/latest/vault_guide/vault.html) can also be used to keep sensitive information hidden and secure. 

## Example : Basic playbook
`nano basic_playbook.yml`

```
- name: "Basic Playbook"
  connection: local
  hosts: localhost
  gather_facts: False


  tasks:
    - name: Create Manufacturer
      netbox.netbox.netbox_manufacturer:
        netbox_url: "{{ lookup('env', 'NETBOX_API') }}"
        netbox_token: "{{ lookup('env', 'NETBOX_TOKEN') }}"
        data:
          name: Juniper
        state: present
```

To run the playbook :  `ansible-playbook basic_playbook.yml`

Output : 
```
PLAY [Basic Playbook] **********************************************************************

TASK [Create Manufacturer] *****************************************************************
ok: [localhost]

PLAY RECAP *********************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
As my database already has the Juniper manufacturer, no changes have been made but the playbook has ran successfully.
