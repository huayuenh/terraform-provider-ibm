![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/IBM-Cloud/terraform-provider-ibm)
![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/IBM-Cloud/terraform-provider-ibm?include_prereleases)
![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/IBM-Cloud/terraform-provider-ibm/release.yml?label=build)
![GitHub](https://img.shields.io/github/license/IBM-Cloud/terraform-provider-ibm)<br />
![GitHub contributors](https://img.shields.io/github/contributors/IBM-Cloud/terraform-provider-ibm?color=blueviolet)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/IBM-Cloud/terraform-provider-ibm?color=blueviolet)
![GitHub all releases](https://img.shields.io/github/downloads/IBM-Cloud/terraform-provider-ibm/total)
[![GitHub stars](https://img.shields.io/github/stars/IBM-Cloud/terraform-provider-ibm?color=yellow)](https://github.com/IBM-Cloud/terraform-provider-ibm/stargazers)

# Terraform Provider

- Website: https://www.terraform.io
- [![Gitter chat](https://badges.gitter.im/hashicorp-terraform/Lobby.png)](https://gitter.im/hashicorp-terraform/Lobby)
- Mailing list: [Google Groups](http://groups.google.com/group/terraform-tool)

## Requirements

-	[Terraform](https://www.terraform.io/downloads.html) 0.10.1+
-	[Go](https://golang.org/doc/install) 1.18 (to build the provider plugin)

## Building The Provider

Clone repository
```sh
git clone git@github.com:IBM-Cloud/terraform-provider-ibm.git
```
Enter the provider directory and build the provider
```sh
cd terraform-provider-ibm
make build
```

## Docker Image For The Provider

You can also pull the docker image for the ibmcloud terraform provider :

```sh
docker pull ibmterraform/terraform-provider-ibm-docker
```

## Download the Provider from the [Terraform Registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest) (Option 1)

Complete the following steps to configure the IBM Cloud provider plug-in for Terraform v0.13 and newer versions.

1. [Download and install Terraform for your system](https://www.terraform.io/intro/getting-started/install.html). 

2. Create a `versions.tf` file in in your Terraform module folder and add a `terraform` block using the syntax below. Note, you must be using Terraform v0.13.x or a newer version.
```
 terraform {
   required_providers {
      ibm = {
         source = "IBM-Cloud/ibm"
         version = "<provider version>"
      }
    }
  }
```

3. Run `terraform init` to fetch the IBM Cloud provider plug-in for Terraform from the Terraform Registry.

## Download the Provider Manually (Option 2)

If you want to run Terraform with the IBM Cloud provider plugin on your system, complete the following steps:

1. [Download and install Terraform for your system](https://www.terraform.io/intro/getting-started/install.html). 

2. [Download the IBM Cloud provider plugin for Terraform](https://github.com/IBM-Bluemix/terraform-provider-ibm/releases).

3. Unzip the release archive to extract the plugin binary (`terraform-provider-ibm_vX.Y.Z`).

4. Move the binary into the Terraform [plugins directory](https://www.terraform.io/docs/configuration/providers.html#third-party-plugins) for the platform.
    - Linux/Unix/OS X: `~/.terraform.d/plugins`
    - Windows: `%APPDATA%\terraform.d\plugins`

5. Export API credential tokens as environment variables. This can either be [IBM Cloud API keys](https://cloud.ibm.com/iam#/users) or Softlayer API keys and usernames, depending on the resources you are provisioning.

```sh
export IC_API_KEY="IBM Cloud API Key"
export IAAS_CLASSIC_API_KEY="IBM Cloud Classic Infrastructure API Key"
export IAAS_CLASSIC_USERNAME="IBM Cloud Classic Infrastructure username associated with Classic Infrastructure API KEY".
```

6. Add the plug-in provider to the Terraform configuration file.

```
provider "ibm" {}
```

See the [official documentation](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started) for more details on using the IBM provider.

## Developing the Provider

If you wish to work on the provider, you'll first need [Go](http://www.golang.org) installed on your machine (version 1.8+ is *required*). You'll also need to correctly setup a [GOPATH](http://golang.org/doc/code.html#GOPATH), as well as adding `$GOPATH/bin` to your `$PATH`.

To compile the provider, run `make build`. This will build the provider and put the provider binary in the `$GOPATH/bin` directory.

```sh
make build
...
$GOPATH/bin/terraform-provider-ibm
...
```

In order to test the provider, you can simply run `make test`.

```sh
make test
```

In order to run the full suite of Acceptance tests, run `make testacc`.

*Note:* Acceptance tests create real resources, and often cost money to run.

```sh
make testacc
```
In order to run a particular Acceptance test, export the variable `TESTARGS`. For example

```sh
export TESTARGS="-run TestAccIBMNetworkVlan_Basic"
```
Issuing `make testacc` will now run the testcase with names matching `TestAccIBMNetworkVlan_Basic`. This particular testcase is present in
`ibm/resource_ibm_network_vlan_test.go`

You will also need to export the following environment variables for running the Acceptance tests.
* `IC_API_KEY`- The IBM Cloud API Key
* `IC_REGION` - The IBM Cloud [region](https://cloud.ibm.com/docs/overview?topic=overview-locations) used by test resources - defaults to `us-south`
* `IAAS_CLASSIC_API_KEY` - The IBM Cloud Classic Infrastructure API Key
* `IAAS_CLASSIC_USERNAME` - The IBM Cloud Classic Infrastructure username associated with the Classic InfrastAPI Key.

Additional environment variables may be required depending on the tests being run. Check console log for warning messages about required variables. 

Alternatively, look for the name of the function by PreCheck under the specific test case and inspect [ibm/acctest/acctest.go](https://github.com/IBM-Cloud/terraform-provider-ibm/blob/master/ibm/acctest/acctest.go) to find the list of environment variables required for the test.

```
	resource.Test(t, resource.TestCase{
		PreCheck:     func() { acc.TestAccPreCheck(t) },
		Providers:    acc.TestAccProviders,
```

## Related projects

### Ansible Collection for IBM Cloud

An Ansible Collection package contains many Ansible Modules,
each Ansible Module is a wrapper around resource or data source
elements of the **Terraform Provider for IBM Cloud**.
At each execution of an Ansible Module, on-the-fly Terraform
code is generated and executed for the intended outcome.

Compatible with Ansible Core 2.12+, various
[example Ansible Playbooks](https://github.com/IBM-Cloud/ansible-collection-ibm#example-ansible-playbooks)
are provided to show how to use
the Ansible Modules from the Ansible Collection for IBM Cloud.

See more information on the package index entry
[ibm.cloudcollection Ansible Collection - Ansible Galaxy](https://galaxy.ansible.com/ui/repo/published/ibm/cloudcollection).

[IBM Cloud Terraform Provider]: https://github.com/IBM-Cloud/terraform-provider-ibm
[Python3]: https://www.python.org/downloads/
[RedHat Ansible]: https://www.ansible.com/
[Ansible search path]: https://docs.ansible.com/ansible/latest/dev_guide/overview_architecture.html#ansible-search-path
[release page]:https://github.com/IBM-Cloud/terraform-provider-ibm/releases

