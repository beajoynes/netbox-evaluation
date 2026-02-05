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


# Custom links
Custom links allow users to display arbitrary hyperlinks to external content within NetBox object views. These are helpful for cross-referencing related records in systems outside NetBox. For example, you might create a custom link on the device view which links to the current device in a Network Monitoring System (NMS).

Custom links are created by navigating to Customization > Custom Links. Each link is associated with a particular NetBox object type (site, device, prefix, etc.) and will be displayed on relevant views. Each link has display text and a URL, and data from the NetBox item being viewed can be included in the link using Jinja template code through the variable object, and custom fields through object.cf.


# Tags
Tags are user-defined labels which can be applied to a variety of objects within NetBox. They can be used to establish dimensions of organization beyond the relationships built into NetBox. For example, you might create a tag to identify a particular ownership or condition across several types of objects.

Fields
* **Name** : A unique human-friendly label for the tag.
*  **Slug** : A unique URL-friendly identifier. (This value will be used for filtering.) This is automatically generated from the tag's name, but can be altered as needed.
* **Color** : The color to use when displaying the tag in the NetBox UI.
* Weight : A numeric weight employed to influence the ordering of tags. Tags with a lower weight will be listed before those with higher weights. Values must be within the range 0 to 32767.
* Object Types : The assignment of a tag may be limited to a prescribed set of objects. For example, it may be desirable to limit the application of a specific tag to only devices and virtual machines.
If no object types are specified, the tag will be assignable to any type of object.
