---
layout: "pagerduty"
page_title: "PagerDuty: pagerduty_schedule"
sidebar_current: "docs-pagerduty-datasource-schedule"
description: |-
  Provides information about a Schedule.

  This data source can be helpful when a schedule is handled outside Terraform but you still want to reference it in other resources.
---

# pagerduty\_schedule

Use this data source to get information about a specific [schedule][1] that you can use for other PagerDuty resources.

## Example Usage

```hcl
data "pagerduty_schedule" "test" {
  name = "Daily Engineering Rotation"
}

resource "pagerduty_escalation_policy" "foo" {
  name      = "Engineering Escalation Policy"
  num_loops = 2

  rule {
    escalation_delay_in_minutes = 10

    target {
      type = "schedule"
      id   = data.pagerduty_schedule.test.id
    }
  }
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name to use to find a schedule in the PagerDuty API.

## Attributes Reference
* `id` - The ID of the found schedule.
* `name` - The short name of the found schedule.

[1]: https://developer.pagerduty.com/api-reference/reference/REST/openapiv3.json/paths/~1schedules~1%7Bid%7D/get
