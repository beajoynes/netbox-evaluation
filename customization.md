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
