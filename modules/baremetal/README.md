## Baremetal Module

### Usage

Creates a single Bare Metal server on the provided subnet.

```hcl
terraform {
  required_version = ">= 1.9.0"
  required_providers {
    ibm = {
      source  = "IBM-Cloud/ibm"
      version = "X.Y.Z"  # Lock into a provider version that satisfies the module constraints
    }
  }
}

locals {
    region = "eu-gb"
}

provider "ibm" {
  ibmcloud_api_key = ""  # replace with apikey value
  region           = local.region
}

module "slz_baremetal" {
  source            = "terraform-ibm-modules/bare-metal-vpc/ibm//modules/baremetal"
  version           = "X.X.X" # Replace "X.X.X" with a release version to lock
  prefix            = "slz-bms"
  profile           = "cx2d-metal-96x192"
  image_id          = "r022-a327ec71-6f38-4bdc-99c8-33e723786a91"
  subnet_ids        = ["r022-d72dc796-b08a-4f8e-a5aa-6c523284173d","r092-d72ddcds96-b0sa-4f8e-a5aa-6c523284s173d"]
  ssh_key_ids       = ["r022-89b37a2e-e78d-46b8-8989-5f8d00cd44d2"]
  bandwidth         = 100000
  allowed_vlans_ids = ["100", "102"]
  access_tags       = null
  resource_group_id = "xxxxxxxxxxxxxxxxx"
}
```

 <!-- The following content is automatically populated by the pre-commit hook -->
 <!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
### Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.9.0 |
| <a name="requirement_ibm"></a> [ibm](#requirement\_ibm) | >= 1.75.2, < 2.0.0 |

### Modules

No modules.

### Resources

| Name | Type |
|------|------|
| [ibm_is_bare_metal_server.bms](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_bare_metal_server) | resource |
| [ibm_is_virtual_network_interface.bms](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_network_interface) | resource |
| [ibm_is_subnet.subnet](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet) | data source |

### Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_access_tags"></a> [access\_tags](#input\_access\_tags) | A list of access management tags to be attached to the bare metal server for categorization and policy enforcement. | `list(string)` | `[]` | no |
| <a name="input_allowed_vlan_ids"></a> [allowed\_vlan\_ids](#input\_allowed\_vlan\_ids) | A list of VLAN IDs that are permitted for the bare metal server, ensuring network isolation and control. Example: [100, 102] | `list(number)` | `[]` | no |
| <a name="input_bandwidth"></a> [bandwidth](#input\_bandwidth) | The allocated bandwidth (in Mbps) for the bare metal server to manage network traffic. If unset, default values apply. | `number` | `null` | no |
| <a name="input_create_timeout"></a> [create\_timeout](#input\_create\_timeout) | Timeout for creating the bare metal server | `string` | `"60m"` | no |
| <a name="input_delete_timeout"></a> [delete\_timeout](#input\_delete\_timeout) | Timeout for deleting the bare metal server | `string` | `"60m"` | no |
| <a name="input_image_id"></a> [image\_id](#input\_image\_id) | The unique identifier of the operating system image to be installed on the bare metal server. | `string` | n/a | yes |
| <a name="input_name"></a> [name](#input\_name) | The base name for the bare metal servers and its resources. | `string` | n/a | yes |
| <a name="input_profile"></a> [profile](#input\_profile) | The hardware profile defining the CPU, memory, and storage configuration of the bare metal server. | `string` | n/a | yes |
| <a name="input_resource_group_id"></a> [resource\_group\_id](#input\_resource\_group\_id) | ID of the resource group where you want to create the service. | `string` | `null` | no |
| <a name="input_security_group_ids"></a> [security\_group\_ids](#input\_security\_group\_ids) | IDs of additional security groups to be added to BMS deployment primary interface. A BMS interface can have a maximum of 5 security groups. | `list(string)` | `[]` | no |
| <a name="input_ssh_key_ids"></a> [ssh\_key\_ids](#input\_ssh\_key\_ids) | A list of SSH key IDs that will be used for secure access to the bare metal server. | `list(string)` | n/a | yes |
| <a name="input_subnet_id"></a> [subnet\_id](#input\_subnet\_id) | A list of subnet IDs where the bare metal server will be deployed, ensuring proper network segmentation. | `string` | n/a | yes |
| <a name="input_update_timeout"></a> [update\_timeout](#input\_update\_timeout) | Timeout for updating the bare metal server | `string` | `"60m"` | no |
| <a name="input_user_data"></a> [user\_data](#input\_user\_data) | User data to initialize BMS deployment | `string` | n/a | yes |

### Outputs

| Name | Description |
|------|-------------|
| <a name="output_baremetal_server_id"></a> [baremetal\_server\_id](#output\_baremetal\_server\_id) | Output for baremetal servers ID. |
| <a name="output_baremetal_server_ip"></a> [baremetal\_server\_ip](#output\_baremetal\_server\_ip) | Output for baremetal IP address. |
| <a name="output_baremetal_server_name"></a> [baremetal\_server\_name](#output\_baremetal\_server\_name) | Output for baremetal servers name. |
| <a name="output_baremetal_server_vni_id"></a> [baremetal\_server\_vni\_id](#output\_baremetal\_server\_vni\_id) | Output for virtual network interface ID. |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
