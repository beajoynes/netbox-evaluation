NetBox docker : https://github.com/netbox-community/netbox-docker

### Quickstart
> **NOTE** : Use alternative wifi to T CORP if in office (E.g. The Point Guest)
```
git clone -b release https://github.com/netbox-community/netbox-docker.git
cd netbox-docker
# Copy the example override file
cp docker-compose.override.yml.example docker-compose.override.yml
```
Read and edit the file to your liking.

* Added `SUPERUSER` to override yaml as it keesp the super user details through restarts.
* Add in `healthcheck:` with `start_period: 150s` as on start up netbox container will have an error if
* the other containers haven't finished setting up first.

```
docker compose pull
docker compose up 
```
Use `-d` after `docker compose up` to allow for detatched startup so containers are run in the background.

> **NOTE** : After initial pull, using the office `T CORP` wifi should work fine for `docker compose up`


### Navigate to webpage

http://172.28.227.204:8000

## Upgrade
When a new upgrade of Netbox is available, a pop up appears at the top of the webpage
<img width="556" height="239" alt="image" src="https://github.com/user-attachments/assets/b8bdb9f2-5aa4-4934-9aca-c4a2ca8f31bc" />

> :warning: **Warning** ⚠️
> be sure to create a [backup](https://github.com/beajoynes/netbox-evaluation/blob/main/backup_restore.md) of the database and
> media before upgrading!

```
git checkout release &&
git pull -p origin release
```
To upgrade, `nano docker-compose.yml` and change `image: docker.io/netboxcommunity/netbox:${VERSION-v4.4-3.4.1}`
to `image: docker.io/netboxcommunity/netbox:${VERSION-v4.4.6-3.4.1}` and save.
```
docker compose pull
docker compose up -d
```
