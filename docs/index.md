---
page_title: "Provider: Cedar"
description: |-
  The Cedar provider is used to configure Cedar authorization policies.
---

This provider exposes a Terraform Data Source for authoring Cedar policies:

```terraform
data "cedar_policyset" "example" {
  policy {
    effect = "permit"

    principal_in = {
      type = "Group"
      id   = "admins"
    }
    action = {
      type = "Action"
      id   = "Read"
    }
    any_resource = true

    when {
      text = "resource.is_public"
    }
    unless {
      text = "resource.owner == User::"alice"
    }
}
```

The `data.cedar_policyset.example.text` output will be:

```
permit (
    principal in Group::"admins",
    action == Action::"Read",
    resource,
)
when {
    resource.is_public
}
unless {
    resource.owner == User::"alice"
};
```

For more information, read the [Cedar documentation](https://docs.commonfate.io).

This Terraform provider was created by [Common Fate](https://commonfate.io). We've built an access management platform based on Cedar. [Read our documentation](https://docs.commonfate.io) or [get in touch](mailto:hello@commonfate.io) if you'd like to learn more.