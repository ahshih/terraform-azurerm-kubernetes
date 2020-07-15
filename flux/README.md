# Azure - Kubernetes Flux Module

## Introduction

This module will enable flux within a managed Kubernetes cluster hosted on Azure Kubernetes Service.
<br />

<!--- BEGIN_TF_DOCS --->
## Providers

| Name | Version |
|------|---------|
| azuread | n/a |
| azurerm | n/a |
| helm | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:-----:|
| aad\_pod\_identity\_version | Azure AD pod identity helm chart version | `string` | `"1.6.0"` | no |
| resource\_group\_name | Resource group name | `string` | n/a | yes |
| service\_principal\_name | Azure Service Principal Name | `string` | n/a | yes |

## Outputs

No output.
<!--- END_TF_DOCS --->
## Example

~~~~
module "flux" {
  source = "github.com/Azure-Terraform/terraform-azurerm-kubernetes.git//flux"

  providers = {helm = helm.aks, kubernetes = kubernetes.aks}

  flux_helm_chart_version = "1.4.0"

  config_repo_ssh_key = tls_private_key.config.private_key_pem
  config_repo_url     = "git@github.com:org/flux.git"
  config_repo_path    = "aks"

  default_ssh_key = tls_private_key.default.private_key_pem
}
~~~~