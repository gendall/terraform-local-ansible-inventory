# Local Ansible Inventory

A Terraform module that will render groups of server IP addresses into an Ansible inventory file and output it to the local filesystem at a specified location.

The module will also take arbitrary secrets (certificates, tokens, keys, etc.) and write them to files in a subdirectory of the output path.

## Usage

```hcl
provider "local" {
  version = "~> 1.3"
}

module "inventory_production" {
  source  = "gendall/ansible-inventory/local"
  servers = {     
    manager = ["1.2.3.4"]
    worker = ["11.22.33.44", "55.66.77.88"]
  }
  secrets = {
    tls_key  = "-----BEGIN RSA PRIVATE KEY----- MIIEow..."
    tls_cert = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQD..."
  }
  output  = "inventory/production"
}
```

## Deployment

This role will be automatically built and deployed to [Terraform Registry](https://registry.terraform.io/modules/gendall) when a [Semver](https://semver.org) tag is pushed to the repo.
