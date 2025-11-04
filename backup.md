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

# Backups
## One time backup onto current local machine (VM)
### Netbox database (postgres)
Create a snapshot of current database, save to file 'netbox_backup.sql'

`docker exec -it netbox-docker-postgres-1 pg_dump -U netbox -h localhost netbox > /tmp/netbox_backup.sql`

Copy the backup from the database container to a newly created (mkdir backups) backups directory

```
$ docker cp netbox-docker-postgres-1:/tmp/netbox_backup.sql ~/git/netbox-docker/backups/netbox_db_backup.sql

Successfully copied 1.33MB to /home/bea/git/netbox-docker/backups/netbox_db_backup.sql
```

Create a compressed tar archive with the specified name/file path from the specified file (path)

`tar czvf ~/git/netbox-docker/backups/netbox_db_backup.sql.tar.gz ~/git/netbox-docker/backups/netbox_db_backup.sql`
```
bea@localhost:~/git/netbox-docker/backups$ ls -al
total 1424
drwxr-xr-x.  2 bea bea      69 Nov  4 11:52 .
drwxr-xr-x. 12 bea bea    4096 Nov  4 11:48 ..
-rw-r--r--.  1 bea bea 1329551 Nov  4 11:40 netbox_db_backup.sql
-rw-r--r--.  1 bea bea  122275 Nov  4 11:52 netbox_db_backup.sql.tar.gz
```
### Netbox media 
Create a compressed tar archive within container

`docker exec -it netbox-docker-netbox-1 tar czvf /tmp/netbox_media_backup.tar.gz /opt/netbox/netbox/media`
```
bea@localhost:~/git/netbox-docker/backups$ docker exec -it netbox-docker-netbox-1 bash
unit@db44dc0ef073:/opt/netbox/netbox$ cd /tmp
unit@db44dc0ef073:/tmp$ ls -al
total 4
drwxrwxrwt. 1 root root  40 Nov  4 12:03 .
drwxr-xr-x. 1 root root  39 Nov  4 11:03 ..
-rw-r--r--. 1 unit root 254 Nov  4 12:03 netbox_media_backup.tar.gz
```
Copy media backup tar archive from conteiner to local backup directory
```
$ docker cp netbox-docker-netbox-1:/tmp/netbox_media_backup.tar.gz  ~/git/netbox-docker/backups/netbox_media_backup.tar.gz`
Successfully copied 2.05kB to /home/bea/git/netbox-docker/backups/netbox_media_backup.tar.gz
```

## Automatic backups using crontab

To create cron job (on some, you are given an option for editor, in Alma I used 'export EDITOR=nano' to set my environment editor to nano as I wa snot used to vi editor.

`crontab -e`

Run netbox_backup.sh every hour at 20minutes past the hour, with a silenced out put. Alternatively use >/tmp/crontab.txt .
```
20 * * * * /home/mickm/netbox_backup.sh >/dev/null 2>&1
```


# Restores
