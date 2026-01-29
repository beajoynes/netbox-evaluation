# **AWX Process Overview**

## **Workflow for Running a Job**

1. **Update the linked repository**  
   Make changes to the repository linked to your AWX project (e.g., edit your playbook or roles).

2. **Sync the project**  
   A project sync fetches the latest content from your source control (e.g., GitHub).  
   - You can enable **“Update revision on launch”** when creating or editing the project to automatically pull the latest code before every job run.

3. **(Re)launch the job from Templates**  
   Once the project is synced, trigger the job template.  
   
   ⚠️ *This cycle can be slow for debugging or iterative testing, though automatic project synchronization is useful for keeping playbooks current.*

---

## **Updating an Inventory Source**

If you modify the inventory file in the linked Git repository:

1. **Sync the Project**  
   Ensure the project is up to date so AWX can load the latest version of the inventory source.

2. **Sync the Inventory Source**  
   From AWX UI or API, sync the inventory source. This pulls in host definitions and variables.

   - New hosts will be **added** automatically.  
   - Existing hosts will **remain** even if removed from the source (AWX does not auto-delete them).  
   - If you **rename** a host in your inventory file, the new name will appear **in addition** to the old one — you’ll need to manually remove the outdated host.

💡 *Tip:* You can configure AWX to automatically delete missing hosts by enabling **“Overwrite”** and **“Overwrite Variables”** options in the inventory source settings.

---

## **Creating a New Job Template**

When creating a new job template in AWX:

- **Name:** A descriptive title for easier identification.  ALso can add a description for further information.
- **Inventory:** Must correspond with the `hosts` value defined in your playbook.  
- **Project:** Select the project linked to your repository.  
- **Playbook:** Choose the specific YAML file path within that project.  
- **Credentials (optional):** Provide required credentials such as SSH keys, vault passwords, or cloud provider tokens.  
- **Execution Environment (optional):** Choose or define an execution environment that has the necessary Ansible collections and dependencies.

✅ *Save & Launch the job when ready.*

---

## **About `ansible_user` and Permissions**

- `ansible_user` must have sufficient permissions to perform all tasks defined in the playbook.  
- AWX job runs inside a **Kubernetes pod** (or container), so it does **not inherit environment variables** or access the user’s home directory from the host.  
- A common workaround for file access issues is to use the `/tmp` directory, which is **world-writable** inside the container.  
- Note that **`connection: local`** does not behave as expected inside an AWX container — it executes locally in the AWX pod, not on the control node.

💡 *For local actions, consider using `delegate_to: localhost` with appropriate context or design tasks to run on the intended control host.*

---


## **Ansible playbooks**
* Expressed in YAML format with a minimum of syntax (See https://docs.ansible.com/projects/ansible/latest/reference_appendices/YAMLSyntax.html#yaml-syntax)
* Idempotent
* Plays - target different hosts with different users
* Tasks - different jobs on the target hosts (within a play)
EXAMPLE
```
---
- name: Update web servers
  hosts: webservers
  remote_user: root

  tasks:
  - name: Ensure apache is at the latest version
    ansible.builtin.yum:
      name: httpd
      state: latest

  - name: Write the apache config file
    ansible.builtin.template:
      src: /srv/httpd.j2
      dest: /etc/httpd.conf

- name: Update db servers
  hosts: databases
  remote_user: root

  tasks:
  - name: Ensure postgresql is at the latest version
    ansible.builtin.yum:
      name: postgresql
      state: latest

  - name: Ensure that postgresql is started
    ansible.builtin.service:
      name: postgresql
      state: started
```
