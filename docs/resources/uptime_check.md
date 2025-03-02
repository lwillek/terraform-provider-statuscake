---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "statuscake_uptime_check Resource - terraform-provider-statuscake"
subcategory: ""
description: |-
  
---

# statuscake_uptime_check (Resource)



## Example Usage

```terraform
resource "statuscake_uptime_check" "example_com" {
  name           = "Example"
  check_interval = 30
  confirmation   = 3
  trigger_rate   = 10

  contact_groups = [
    statuscake_contact_group.operations_team.id
  ]

  http_check {
    enable_cookies   = true
    follow_redirects = true
    timeout          = 20
    user_agent       = "terraform managed uptime check"
    validate_ssl     = true

    basic_authentication {
      username = "username"
      password = "password"
    }

    content_matchers {
      content         = "Welcome"
      include_headers = true
      matcher         = "CONTAINS_STRING"
    }

    request_headers = {
      Authorization = "bearer 123456"
    }

    status_codes = [
      "202",
      "404",
      "405",
    ]
  }

  monitored_resource {
    address = "https://www.example.com"
  }

  regions = [
    "london",
    "london",
    "paris",
  ]

  tags = [
    "production",
  ]
}

output "example_com_uptime_check_id" {
  value = statuscake_uptime_check.example_com.id
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **check_interval** (Number) Number of seconds between checks
- **monitored_resource** (Block List, Min: 1, Max: 1) Monitored resource configuration block. The describes server under test (see [below for nested schema](#nestedblock--monitored_resource))
- **name** (String) Name of the check

### Optional

- **confirmation** (Number) Number of confirmation servers to confirm downtime before an alert is triggered
- **contact_groups** (Set of String) List of contact group IDs
- **dns_check** (Block List, Max: 1) DNS check configuration block. Only one of `dns_check`, `http_check`, `icmp_check`, and `tcp_check` may be specified (see [below for nested schema](#nestedblock--dns_check))
- **http_check** (Block List, Max: 1) HTTP check configuration block. Only one of `dns_check`, `http_check`, `icmp_check`, and `tcp_check` may be specified (see [below for nested schema](#nestedblock--http_check))
- **icmp_check** (Block List, Max: 1) ICMP check configuration block. Only one of `dns_check`, `http_check`, `icmp_check`, and `tcp_check` may be specified (see [below for nested schema](#nestedblock--icmp_check))
- **id** (String) The ID of this resource.
- **paused** (Boolean) Whether the check should be run
- **regions** (List of String) List of regions on which to run checks. The values required for this parameter can be retrieved from the `GET /v1/uptime-locations` endpoint
- **tags** (Set of String) List of tags
- **tcp_check** (Block List, Max: 1) TCP check configuration block. Only one of `dns_check`, `http_check`, `icmp_check`, and `tcp_check` may be specified (see [below for nested schema](#nestedblock--tcp_check))
- **trigger_rate** (Number) The number of minutes to wait before sending an alert

### Read-Only

- **locations** (Set of Object) List of assigned monitoring locations on which to run checks (see [below for nested schema](#nestedatt--locations))

<a id="nestedblock--monitored_resource"></a>
### Nested Schema for `monitored_resource`

Required:

- **address** (String) URL, FQDN, or IP address of the server under test

Optional:

- **host** (String) Name of the hosting provider


<a id="nestedblock--dns_check"></a>
### Nested Schema for `dns_check`

Required:

- **dns_ips** (Set of String) List of IP addresses to compare against returned DNS records

Optional:

- **dns_server** (String) FQDN or IP address of the nameserver to query


<a id="nestedblock--http_check"></a>
### Nested Schema for `http_check`

Required:

- **status_codes** (Set of String) List of status codes that trigger an alert

Optional:

- **basic_authentication** (Block List, Max: 1) Basic Authentication (RFC7235) configuration block (see [below for nested schema](#nestedblock--http_check--basic_authentication))
- **content_matchers** (Block List, Max: 1) Content matcher configuration block. This is used to assert values within the response of the request (see [below for nested schema](#nestedblock--http_check--content_matchers))
- **enable_cookies** (Boolean) Whether to enable cookie storage
- **final_endpoint** (String) Specify where the redirect chain should end
- **follow_redirects** (Boolean) Whether to follow redirects when testing. Disabled by default
- **request_headers** (Map of String) Represents headers to be sent when making requests
- **request_method** (String) Type of HTTP check. Either HTTP, or HEAD
- **request_payload** (Map of String) Payload submitted with the request. Setting this updates the check to use the HTTP POST verb. Only one of `request_payload` or `request_payload_raw` may be specified
- **request_payload_raw** (String) Raw payload submitted with the request. Setting this updates the check to use the HTTP POST verb. Only one of `request_payload` or `request_payload_raw` may be specified
- **timeout** (Number) The number of seconds to wait to receive the first byte
- **user_agent** (String) Custom user agent string set when testing
- **validate_ssl** (Boolean) Whether to send an alert if the SSL certificate is soon to expire

<a id="nestedblock--http_check--basic_authentication"></a>
### Nested Schema for `http_check.basic_authentication`

Required:

- **password** (String, Sensitive)
- **username** (String)


<a id="nestedblock--http_check--content_matchers"></a>
### Nested Schema for `http_check.content_matchers`

Required:

- **content** (String) String to look for within the response. Considered down if not found

Optional:

- **include_headers** (Boolean) Include header content in string match search
- **matcher** (String) Whether to consider the check as down if the content is present within the response



<a id="nestedblock--icmp_check"></a>
### Nested Schema for `icmp_check`

Optional:

- **enabled** (Boolean) Dummy attribute to allow for a nested block. This field should not be changed


<a id="nestedblock--tcp_check"></a>
### Nested Schema for `tcp_check`

Required:

- **port** (Number) Destination port for TCP checks

Optional:

- **authentication** (Block List, Max: 1) Authentication configuration block (see [below for nested schema](#nestedblock--tcp_check--authentication))
- **protocol** (String) Type of TCP check. Either SMTP, SSH or TCP
- **timeout** (Number) The number of seconds to wait to receive the first byte

<a id="nestedblock--tcp_check--authentication"></a>
### Nested Schema for `tcp_check.authentication`

Required:

- **password** (String, Sensitive)
- **username** (String)



<a id="nestedatt--locations"></a>
### Nested Schema for `locations`

Read-Only:

- **description** (String)
- **ipv4** (String)
- **ipv6** (String)
- **region** (String)
- **region_code** (String)
- **status** (String)

## Import

Uptime checks can be imported using the check `id`, e.g.

```
$ terraform import statuscake_uptime_check.example_com 1234
```
