---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-team-spaces'
is: 'future'
---
## Get a list of spaces in your team(s)

A team administrator can obtain a list of spaces in a team as follows:

```
query getTeamSpaces {
  teamSpaces(first: 50, teamIds: ["my-team-id"]) {
    items {
      id
      title
      members {
        items {
          displayName
        }
      }
    }
  }
}
```

A team administrator may need to obtain a list of any spaces without owners (e.g., following an owner's departure from the team)
with a view to assigning new owners. This can be achieved by passing some additional optional parameters to the _teamSpaces_
GraphQL query:
 - `excludingRoles`: List of roles not represented among the membership of the space. In this case, passing a list comprising
   the value `"SPACE_OWNER"` will restrict the query to spaces with no owner.
 - `includingRoles`: List of roles represented among the membership of the space. Not relevant to the present example, but if a
   list of spaces _with_ owners were required instead, `["SPACE_OWNER"]` could be passed here rather than as `excludingRoles`.

```
query getOrphanSpaces {
  teamSpaces(first: 50, teamIds: ["my-team-id"], excludingRoles: ["SPACE_OWNER"]) {
    items {
      id
      title
      members {
        items {
          displayName
        }
      }
    }
  }
}
```
