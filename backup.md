 This aims to document the backup process for Netbox.

 Assumes Netbox is being run using docker containers. 
 With the main containers being netbox-docker-netbox-1 and netbox-docker-postgres-1 (for the database)
I used the [netbox-docker repository](https://github.com/netbox-community/netbox-docker) netbox version : v3.3-2.2.0 
populated with dummy data from the [netbox-demo-data repository](https://github.com/netbox-community/netbox-demo-data), both foudn on the netbox-community github.

From laptop/Ubuntu-24.04 terminal, SSH into local host (in this case my Almalinux virtual machine, AlmaVM) and locate the netbox-docker directory.

`
ssh bea@192.168.0.92

cd git/netbox-docker/
`

Run the continers and navigate to the [netbox page](http://192.168.0.92:8000/) which should be at http://localhost:8000.

`
docker compose up -d

docker ps #check containers are up and running
`
