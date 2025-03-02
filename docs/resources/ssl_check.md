---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "statuscake_ssl_check Resource - terraform-provider-statuscake"
subcategory: ""
description: |-
  
---

# statuscake_ssl_check (Resource)



## Example Usage

```terraform
resource "statuscake_ssl_check" "example_com" {
  check_interval = 600
  user_agent     = "terraform managed SSL check"

  contact_groups = [
    statuscake_contact_group.operations_team.id
  ]

  alert_config {
    alert_at = [7, 14, 21]

    on_reminder = true
    on_expiry   = true
    on_broken   = false
    on_mixed    = false
  }

  monitored_resource {
    address = "https://www.example.com"
  }
}

output "example_com_ssl_check_id" {
  value = statuscake_ssl_check.example_com.id
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **alert_config** (Block List, Min: 1, Max: 1) Alert configuration block (see [below for nested schema](#nestedblock--alert_config))
- **check_interval** (Number) Number of seconds between checks
- **monitored_resource** (Block List, Min: 1, Max: 1) Monitored resource configuration block. The describes server under test (see [below for nested schema](#nestedblock--monitored_resource))

### Optional

- **contact_groups** (Set of String) List of contact group IDs
- **follow_redirects** (Boolean) Whether to follow redirects when testing. Disabled by default
- **id** (String) The ID of this resource.
- **paused** (Boolean) Whether the check should be run
- **user_agent** (String) Custom user agent string set when testing

<a id="nestedblock--alert_config"></a>
### Nested Schema for `alert_config`

Required:

- **alert_at** (Set of Number) List representing when alerts should be sent (days). Must be exactly 3 numerical values

Optional:

- **on_broken** (Boolean) Whether to enable alerts when SSL certificate issues are found
- **on_expiry** (Boolean) Whether to enable alerts when the SSL certificate is to expire
- **on_mixed** (Boolean) Whether to enable alerts when mixed content is found
- **on_reminder** (Boolean) Whether to enable alert reminders


<a id="nestedblock--monitored_resource"></a>
### Nested Schema for `monitored_resource`

Required:

- **address** (String) URL of the server under test

Optional:

- **hostname** (String) Hostname of the server under test

## Import

SSL checks can be imported using the check `id`, e.g.

```
$ terraform import statuscake_ssl_check.example_com 1234
```
