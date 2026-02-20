# Best practice for PTN import

1. fresh netbox instance
2. Adjust configuration.py file as needed to change status field choices
3. Add custom field choices to netbox
4. Add custom fields to netbox
5. Manually add owners, regions, site groups
6. Translate data extract to Netbox friendly csv (using excel sheets)
7. Proof check for correct names!! ETC
8. Upload into netbox using bulk import



## Order for import

1. sites
2. locations
3. racks
4. devices
5. interfaces
6. connections
