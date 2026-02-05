# Custom fields

Each model in NetBox is represented in the database as a table with each attribute of a model a column. 
Create a custom field to hold extra data - stored directly alongside each object as a JSON file.

There are many types of custom fields : 
* Text
* Long text
* Integer
* Decimal
* Boolean
* Date
* Date & Time
* URL
* JSON
* Selection
* Multiple selection
* Object
* Multiple object


Fields need a simple database friendly string as a name, as well as a human friendly name that will be displayed on web forms.

It also requires a weight : higher weights will be ordered lower within a form (default = 100).

## Adding a new custom field 

Fields (Bold = Required) :
* **Object types**
* **Name** - DB friendly, alphanumeric and underscores
* **Type**
* Label
* Group name
* Description
* (Check box) Required
* (Check box) Unique
* Default value
* Validation regex
* **Search weight** (lower = important, 0 = ignore, default = 1000)
* **Filter logic** (loose, disabled, exact)
* **UI visible** (always, if set, hidden)
* **UI editable** (yes, no, hidden)
* **Display weight** (higher = lower in form, default = 100)
* (Check box) Clonable
* Comments
* Changelog


### Screenshots 

<img width="937" height="914" alt="image" src="https://github.com/user-attachments/assets/f7fb8642-cd6b-48c9-877d-b70144448271" />

<img width="927" height="917" alt="image" src="https://github.com/user-attachments/assets/20f544a5-f0e9-4c77-8cbe-cb0af4b51631" />
