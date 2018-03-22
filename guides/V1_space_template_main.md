---
copyright: 'Copyright IBM Corp. 2018'
link: 'space-template-main'
is: 'experimental'
---

# Space Template

In Watson Work Services a space template is a template for the creation of a space.
The space template defines user configurable properties for the space, 
as well as a set of required apps that are automatically added to the space on creation.

# Properties

There are three types of properties in a space template: List, Boolean, and Text.

# Status

Status is a special list style attribute on the template. 
Status consists of a list of values that can be used to describe the state of the space; for example, open, closed, archived.

# Required Apps

Required apps define a set of applications (by ID) that are added to each new space on creation.

# teamId and offeringCollaborationType

teamId and offeringCollaborationType describe the team in which the space will be created.
These values are derived either from the offering with which the template is associated 
(in the case of an offering template) or from the user who created the template 
(in the case of a user-created custom template).