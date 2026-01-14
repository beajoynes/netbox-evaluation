# [JAN 2026] Starting up awx-operator once already installed
```
minikube start
kubectl port-forward svc/awx-demo-service 8090:80 -n awx
```

# [DEC 2025] Setting up a project linked to github (using AWX UI)
This was made in December 2025, in recent releases some of the menu names and layout has changed however I managed to navigate it in Jan 2025 following thiese instructions so will not update this unless there is significant change. **Layout of menu changes between test tech version and the regular UI**
1. **Create an organisation**
   * Navigate to Access Management > Organizations and click 'Create organisation'.
   * Enter a name, I used 'Digital Twin' as I am linking it to the digital twin github.
2. **Add credentials for github**
   As the digital twin github is private, we need to use SSH to access it.
   * Navigate to Access Management > Credentials and click 'Create credential'.
   * Enter a name to identify the credential (I chose 'Github'), pick the organisation from
   * above and select 'Source control' for Credential type.
   * Add your github user (for myself, 'beajoynes') and for the SCM Private Key, copy and paste your private key which matches the public key you have entered in github (I used `cat ~/.ssh/id_ed25519` to find mine).
3. **Create project**
   * Navigate to Projects and click 'Create project'
   * Enter a name (Digital twin)
   * Select your organisation
   * Select your Source Control type as Git, this expands the menu for more options to enter
   * Add in the SSH URL from the github repo (git@github.com:mmorrow24work/digital-twin-containerlab.git), add 'main' as Source Control Branch and select the credential from step 2 as Source Control Credential.
   
# [Jan 2025] Netbox dynamic inventory (using AWX UI)
> [!IMPORTANT]
> BE SURE TO SYNC PROJECT IF CHANGES ARE MADE TO GITHUB!!
1. Create and **record** API token from netbox.
2. Create a YAML file in the project github to use the netbox inventory plugin and access your netbox instance (https://github.com/mmorrow24work/digital-twin-containerlab/blob/main/ANSIBLE/AWX-OPERATOR/BEA/netbox_inventory.yml)
3. Create execution environment (Under 'Administration' in awx menu) - I followed [this video](https://www.youtube.com/watch?v=4YjQmH-osI8) and so used [this image](https://github.com/users/packetstopurpose/packages/container/package/ansible-ee-netbox)
4. Create inventory
   * Navigate to inventories (under Resources in awx UI menu), click add -> Add inventory
   * Add name (Netbox Inventory), description optional
   * Select organisation (Digital Twin)
5. Setup Inventory source (Netbox)
   * Select the newly created 'Netbox Inventory', then select Sources and Add
   * Input the name (Netbox)
   * Select the execution environment created in step 3
   * For Source, select 'Sourced from a project' - more detail options will appear
   * Select the Project (Digital Twin)
   * For Inventory File, copy in the path to the yaml file from step 2
   * Save and Sync
6. Upon successful job (sync), Relevant hosts should appear in Inventories > Netbox Inventory > Hosts
7. **Schedule for dynamic inventory updates**
   * In Netbox Inventory > Sources > Netbox, Navigate to the Schedules header, select Add
   * Add in details as required depending on frequency.

