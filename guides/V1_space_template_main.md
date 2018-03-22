---
copyright: 'Copyright IBM Corp. 2018'
link: 'space-template-main'
is: 'experimental'
---

# Space Template

In Watson Work Services a space template is a template applied to a team space on creation of the space.
The space template defines user configurable properties for the space, 
as well as a set of required apps that are automatically added to the space on creation.

# Properties

There are three types of properties in a space template; List, Boolean, and Text.

# Status

Status is a special list style attribute on the template. 
It can be used to describe the of the space; for example, open, closed, archived.

# Required Apps

Required apps define a set of applications (by ID) that are added to each new space on creation.

# teamId and offeringCollaborationType

teamId and offeringCollaborationType describe in which team the space will be created. 
For an offering template these are based on the offering, 
for a user created template these are based on the current users offering.
