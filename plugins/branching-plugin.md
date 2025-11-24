A netbox plugin that introduces branching functionality - this is now an 'official' NetBoxLabs plugin so it is owned and 
supported fully by NetBox themselves.
Allows for the creation of a discrete snapshot f the NetBox database which can be modified independently before later being
merged back into the `main` branch. Good practice is to lock the `main` branch so everyone wokrs on branches that need 
approval and reviewed before being added to thge main branch to avoid any incvorrect changes being made directly to the main 
branch without interferring with it's integrity.

# Installation

* In `plugin_requirements.txt`, the plugin is named `netboxlabs-netbox-branching`
* In `congifuration/plugins.py`, reference `"netbox_branching"`
* **Unique requirement** : In `configuration/configuration.py`, need to ensure DATABASES is wrapped by `DynamicSchemaDict()`
 and add `DATABASE_ROUTER` after:
  ```
    from netbox_branching.utilities import DynamicSchemaDict

    DATABASES = DynamicSchemaDict({
      'default': {
          'ENGINE': 'django.db.backends.postgresql',
          'NAME': 'netbox',               # Database name
          'USER': 'netbox',               # PostgreSQL username
          'PASSWORD': 'password',         # PostgreSQL password
          'HOST': 'localhost',            # Database server
          'PORT': '',                     # Database port (leave blank for default)
          'CONN_MAX_AGE': 300,            # Max database connection age
      }
    })


    DATABASE_ROUTERS = [
      'netbox_branching.database.BranchAwareRouter',
    ]
  ```

# Test
Working in main branch, option to 'create a branch' : 
<img width="904" height="622" alt="image" src="https://github.com/user-attachments/assets/4896ace8-0743-4d6d-a08c-a161c993dbef" />

'Create a branch' page :
<img width="903" height="792" alt="image" src="https://github.com/user-attachments/assets/f493c1d9-38ad-4105-bd9e-b96427fce76d" />


