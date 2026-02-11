When working in the office, some of the applications we have been looking at as part of the digital twin project will not work when using the office wifi (T-CORP or T-GUEST). 

Until the applications are allowed on the Telent wifi the main work arounds are to connect to :
- The point wifi (The building wifi, rather than Telent's wifi which is restricted)
- Your phone's hotspot


### Office wifi :office:
:heavy_check_mark: Can run ansible playbooks locally

:grey_question: Can I access netbox inventory ? 

:grey_question: Can I access netbox lookup ?

:heavy_check_mark: Can access awx UI (Once already started up)

❔ Can I start minikube to use awx?

:grey_question: Can I Install and setup awx-operator?

:x: awx project sync  

:x: awx job launch/run

:x: `git clone` - Need to use The Point Guest wifi

:heavy_check_mark: `docker compose up -d` to set up Netbox

:heavy_check_mark: Use Netbox UI


## CISCO umbrella 
In **windows powershell** : `Get-Service | Where-Object { $_.DisplayName -like "*Cisco*" -or $_.Name -like "*Cisco*" }`

Output should look like this (if umbrella is running) :
```
Status   Name               DisplayName
------   ----               -----------
Running  csc_swgagent       Cisco Secure Client - Umbrella SWG ...
Running  csc_umbrellaagent  Cisco Secure Client - Umbrella Agent
Running  csc_vpnagent       Cisco Secure Client - AnyConnect VP...
```

### **STOP** umbrella
`Stop-Service -Name "csc_umbrellaagent"`
```
WARNING: Waiting for service 'Cisco Secure Client - Umbrella Agent (csc_umbrellaagent)' to stop...
WARNING: Waiting for service 'Cisco Secure Client - Umbrella Agent (csc_umbrellaagent)' to stop...
```

### **START** umbrella 
`Start-Service -Name "csc_umbrellaagent"`
