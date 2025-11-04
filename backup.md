 This aims to document the backup process for Netbox.

 Assumes Netbox is being run using docker containers. 
 With the main containers being netbox-docker-netbox-1 and netbox-docker-postgres-1 (for the database)
I used the [netbox-docker repository](https://github.com/netbox-community/netbox-docker) netbox version : v3.3-2.2.0 
populated with dummy data from the [netbox-demo-data repository](https://github.com/netbox-community/netbox-demo-data), both foudn on the netbox-community github.

From laptop/Ubuntu-24.04 terminal, SSH into local host (in this case my Almalinux virtual machine, AlmaVM) and locate the netbox-docker directory.

`ssh bea@192.168.0.92`

`cd git/netbox-docker/`


Run the continers and navigate to the [netbox page](http://192.168.0.92:8000/) which should be at http://localhost:8000.

`docker compose up -d`

`docker ps #check containers are up and running`

<img width="959" height="499" alt="image" src="https://github.com/user-attachments/assets/d468145b-2228-455d-825f-4853dad3f114" />


### One time backup onto current local machine (VM)
Create a snapshot of current database, save to file 'netbox_backup.sql'

`docker exec -it netbox-docker-postgres-1 pg_dump -U netbox -h localhost netbox > /tmp/netbox_backup.sql`

Copy the backup from the database container to a newly created (mkdir backups) backups directory

```
$ docker cp netbox-docker-postgres-1:/tmp/netbox_backup.sql ~/git/netbox-docker/backups/netbox_db_backup.sql

Successfully copied 1.33MB to /home/bea/git/netbox-docker/backups/netbox_db_backup.sql
```

Create a compressed tar archive with the specified name/file path from the specified file (path)

`tar czvf ~/git/netbox-docker/backups/netbox_db_backup.sql.tar.gz ~/git/netbox-docker/backups/netbox_db_backup.sql`

