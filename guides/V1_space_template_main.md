---
copyright: 'Copyright IBM Corp. 2018'
link: 'space-template-main'
is: 'experimental'
---

# Space Template

In Watson Work Services a space template is a template for the creation of a space.
The space template defines user configurable properties for the space, 
as well as a set of required apps that are automatically added to the space on creation.

# Key fields

| property      | type          | description  |
| ------------- |:------------- |:-----|
| properties |SpacePropertyCollection |There are three types of properties in a space template: List, Boolean, and Text.|
| status |SpaceStatus |Status is a top-level list style attribute on the template. Status consists of a list of values that can be used to describe the state of the space; for example, open, closed, archived.|
| requiredApps |SpaceRequiredApplicationCollection |Required apps define a set of applications (by ID) that are added to each new space on creation.|
| teamId |String |The id of the team in which the space will be created, derived either from the offering with which the template is associated (in the case of an offering template) or from the user who created the template (in the case of a user-created custom template)|
| offeringCollaborationType |OfferingCollaborationType |The type of offering with which the space will be associated, derived either from the offering with which the template is associated (in the case of an offering template) or from the user who created the template (in the case of a user-created custom template)|
