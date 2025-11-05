 This aims to document the backup and restore process for Netbox.

Useful docs : https://netboxlabs.com/docs/netbox/administration/replicating-netbox/

 Assumes Netbox is being run using docker containers. 
 With the main containers being netbox-docker-netbox-1 and netbox-docker-postgres-1 (for the database)
I used the [netbox-docker repository](https://github.com/netbox-community/netbox-docker) netbox version : v3.3-2.2.0 
populated with dummy data from the [netbox-demo-data repository](https://github.com/netbox-community/netbox-demo-data), both found on the netbox-community github.

From laptop/Ubuntu-24.04 terminal, SSH into local host (in this case my Almalinux virtual machine, AlmaVM) and locate the netbox-docker directory.

`ssh bea@192.168.0.92`

`cd git/netbox-docker/`


Run the continers and navigate to the [netbox page](http://192.168.0.92:8000/) which should be at http://localhost:8000.

`docker compose up -d`

Check containers are all up and running using
`docker ps -a`

<img width="1918" height="997" alt="image" src="https://github.com/user-attachments/assets/8f22c41f-9bf7-430d-898e-95ce69a58c94" />


# Backups
## One time backup onto current local machine (VM)
### Netbox database (postgres)
Create a snapshot of current database, save to file 'netbox_backup.sql'

`docker exec -it netbox-docker-postgres-1 pg_dump -U netbox -h localhost netbox > /tmp/netbox_backup.sql`

Copy the backup from the database container to a newly created (mkdir backups) backups directory

Or just use:
`docker exec -it netbox-docker-postgres-1 pg_dump -U netbox -h localhost netbox > ~/git/netbox-docker/backups/netbox_backup.sql`


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
Copy media backup tar archive from container to local backup directory
```
$ docker cp netbox-docker-netbox-1:/tmp/netbox_media_backup.tar.gz  ~/git/netbox-docker/backups/netbox_media_backup.tar.gz`
Successfully copied 2.05kB to /home/bea/git/netbox-docker/backups/netbox_media_backup.tar.gz
```

## Automatic backups using crontab

Using [Mick's script](https://github.com/mmorrow24work/digital-twin-containerlab/blob/main/NETBOX/netbox_backup.sh) as a base. In ~/git/netbox-docker/backups directory, `touch netbox_backup.sh` then `nano netbox_backup.sh` and copy in the following. Differs with location of backup directory and omitting sudo as it creates issues with for my run.
```
#!/bin/bash

# Define timestamp format for filenames
timestamp=$(date +"%Y%m%d_%H%M")

# Define backup directory
backup_dir=~/git/netbox-docker/backups/auto_backups
mkdir -p "$backup_dir"

# Backup database
docker exec -i netbox-docker-postgres-1 pg_dump -U netbox netbox > "$backup_dir/netbox_postgres_backup_$timestamp.sql"
tar czvf "$backup_dir/"$HOSTNAME"_netbox_postgres_backup_$timestamp.sql.tar.gz" -C "$backup_dir" "netbox_postgres_backup_$timestamp.sql"
rm "$backup_dir/netbox_postgres_backup_$timestamp.sql"

# Backup media files
docker exec netbox-docker-netbox-1 tar czvf /tmp/netbox_media_backup.tar.gz /opt/netbox/netbox/media
docker cp netbox-docker-netbox-1:/tmp/netbox_media_backup.tar.gz "$backup_dir/"$HOSTNAME"_netbox_media_backup_$timestamp.tar.gz"

# Purge backups older than 3 days
find "$backup_dir" -type f -mtime +3 -name "*.tar.gz" -exec rm -f {} \;
```
Make sure the file has execute priviliges using
`chmod +x netbox_backup.sh`

To create cron job (on some, you are given an option for editor, in Alma I used 'export EDITOR=nano' to set my environment editor to nano as I was not used to vi editor).

`crontab -e`

Run netbox_backup.sh every hour at 20minutes past the hour, with a silenced out put. Alternatively use >/tmp/crontab.txt to gather output for troubleshooting (for example) .
```
20 * * * * /home/bea/git/netbox-docker/backups/netbox_backup.sh >/dev/null 2>&1
```
Check this is working by looking into the directory that should be created, files should be made at the time specified.

### Troubleshooting
Check the script works by just running it

`/home/bea/git/netbox-docker/backups/netbox_backup.sh`

Change cron job to 

`52 * * * * /home/bea/git/netbox-docker/backups/netbox_backup.sh >/tmp/crontab.txt 2>&1'

And navigate do cat /tmp/crontab.txt to see output of attempting job

## Backup to another machine (VM)
First follow, [one-time-backup-onto-current-local-machine-(VM)](https://github.com/beajoynes/netbox-evaluation/blob/main/backup_restore.md#one-time-backup-onto-current-local-machine-vm)

For this I have gone from my backups in my Almalinux VM (AlmaVM/localhost) to my google cloud VM (symbo).

In local host (where backups are saved)

`cat /home/beajoynes/.ssh/id_ed25519.pub`

Copy out response (should start ssh-ed25519 AAAA....) and add to `~/.ssh/authorized_keys` in other machine, I attempted to add the public SSH to the google cloud UI but this didn't add to the authorised key file so I used nano and added manually. Save.

Check connection using `ssh user@othervm` the `exit`.

Change to backups directory e.g. `cd /git/netbox-docker/backups/auto_backups`.

Copy the desired backup to tmp directory on the other machine.
```
$ scp localhost.localdomain_netbox_media_backup_20251104_1610.tar.gz beajoynes@34.134.76.112:/tmp
localhost.localdomain_netbox_media_backup_20251104_1610.t 100%  254     2.3KB/s   00:00
```
Check other machine has received back up. Repeat for both postgres and media backup.

Note the backup can be copied to any file in the other machine (for example create a file for backups `mkdir ~/netbox_backups`.

### SSH issues
I had an issue with connection between my google cloud test1 VM and my parrot OS VM. After attempting different options of troubleshooting, I ended up using ssh the other way round : 

` scp beajoynes@34.39.10.82:/path/to/backup.tar.gz /local/path/ `

# Restores

Extract the compressed tar archive of the backup you wish to restore. If you haven't already, use `git clone https://github.com/netbox-community/netbox-docker.git` to download the netbox-docker repository. Creates .sql file.
```
tar xzvf /tmp/localhost.localdomain_netbox_postgres_backup_20251104_1700.sql.tar.gz -C /tmp   
cd ~/git/netbox-docker
docker compose up -d
```
<img width="1840" height="1069" alt="image" src="https://github.com/user-attachments/assets/95581401-9191-49da-8f88-68aaa9998474" />


```
docker stop netbox-docker-netbox-1
docker exec -it netbox-docker-postgres-1 psql -U netbox -d postgres -c "DROP DATABASE netbox;"
docker exec -it netbox-docker-postgres-1 psql -U netbox -d postgres -c "CREATE DATABASE netbox OWNER netbox;"


cat /tmp/netbox_backup.sql | docker exec -i netbox-docker-postgres-1 psql -U netbox -d netbox
docker compose down
docker compose up -d
docker ps
```

Navigate to other virtual machine's netbox server   http://34.134.76.112:8000

<img width="1827" height="1068" alt="image" src="https://github.com/user-attachments/assets/c2323784-386c-43d0-a8ae-da11fed1af5a" />
