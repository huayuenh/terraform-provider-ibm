---
layout: "ibm"
page_title: "IBM : ibm_cd_toolchain_tool_bitbucketgit"
description: |-
  Get information about cd_toolchain_tool_bitbucketgit
subcategory: "Continuous Delivery"
---

# ibm_cd_toolchain_tool_bitbucketgit

Provides a read-only data source to retrieve information about a cd_toolchain_tool_bitbucketgit. You can then reference the fields of the data source in other resources within the same configuration by using interpolation syntax.

See the [tool integration](https://cloud.ibm.com/docs/ContinuousDelivery?topic=ContinuousDelivery-bitbucket) page for more information.

## Example Usage

```hcl
data "ibm_cd_toolchain_tool_bitbucketgit" "cd_toolchain_tool_bitbucketgit" {
	tool_id = "9603dcd4-3c86-44f8-8d0a-9427369878cf"
	toolchain_id = data.ibm_cd_toolchain.cd_toolchain.id
}
```

## Argument Reference

You can specify the following arguments for this data source.

* `tool_id` - (Required, Forces new resource, String) ID of the tool bound to the toolchain.
  * Constraints: The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-4[a-fA-F0-9]{3}-[89abAB][a-fA-F0-9]{3}-[a-fA-F0-9]{12}$/`.
* `toolchain_id` - (Required, Forces new resource, String) ID of the toolchain.
  * Constraints: The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-4[a-fA-F0-9]{3}-[89abAB][a-fA-F0-9]{3}-[a-fA-F0-9]{12}$/`.

## Attribute Reference

After your data source is created, you can read values from the following attributes.

* `id` - The unique identifier of the cd_toolchain_tool_bitbucketgit.
* `crn` - (String) Tool CRN.
* `href` - (String) URI representing the tool.
