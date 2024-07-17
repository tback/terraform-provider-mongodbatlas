# Data Source: mongodbatlas_org_invitation

`mongodbatlas_org_invitation` describes an invitation for a user to join an Atlas organization.

## Example Usage

```terraform
resource "mongodbatlas_org_invitation" "test" {
  username    = "test-acc-username"
  org_id      = "<ORG-ID>"
  roles       = [ "GROUP_DATA_ACCESS_READ_WRITE" ]
}

data "mongodbatlas_org_user" "test" {
  org_id     = mongodbatlas_org_user.test.org_id
  username   = mongodbatlas_org_user.test.username
}
```

## Argument Reference

* `org_id` - (Required) Unique 24-hexadecimal digit string that identifies the organization to which you invited the user.
* `username` - (Required) Email address of the invited user. This is the address to which Atlas sends the invite. If the user accepts the invitation, they log in to Atlas with this username.
* `invitation_id` - (Required) Unique 24-hexadecimal digit string that identifies the invitation in Atlas.

## Attributes Reference

In addition to the arguments, this data source exports the following attributes:

* `id` - Autogenerated unique string that identifies this data source.
* `created_at` - Timestamp in ISO 8601 date and time format in UTC when Atlas sent the invitation.
* `expires_at` - Timestamp in ISO 8601 date and time format in UTC when the invitation expires. Users have 30 days to accept an invitation.
* `inviter_username` - Atlas user who invited `username` to the organization.
* `teams_ids` - An array of unique 24-hexadecimal digit strings that identify the teams that the user was invited to join.
* `roles` - Atlas roles to assign to the invited user. If the user accepts the invitation, Atlas assigns these roles to them. The [MongoDB Documentation](https://www.mongodb.com/docs/atlas/reference/user-roles/#organization-roles) describes the roles a user can have.

See the [MongoDB Atlas Administration API](https://docs.atlas.mongodb.com/reference/api/organization-get-one-invitation/) documentation for more information.