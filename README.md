# Azure
about azure: https://learn.microsoft.com/en-us/training/paths/azure-sql-fundamentals/

# Create a virtual machine

## Basics

Project details

- Subscription: `Azure for Students`
- Resource group: `(New) test_vm_group`

Instance details:

- Virtual Machine name `test-vm`
- Region `(Europe) Sweden Central`
- Availability options `No infrastructure redundancy required`
- Security type `Trusted launch virtual machines`
- Image `Debian 12 "bookworm" - x64 Gen2`
- VM architecture `x64`
- Run with Azure Spot discount `off`
- Size `Standard_B1s`
- Enable Hibernation (preview) `off`


Administrator account

- Authentication type `SSH public key`
- Username `azureuser`
- SSH public key source: `Use existing public key`
  ```
  ssh-keygen -t rsa -b 4096 -f ~/.ssh/my_ssh_key
  cat ~/.ssh/my_ssh_key.pub
  ```

Inbound port rules

- Public inbound ports `Allow selected ports`
- Select inbound ports `SSH (22)`

## Disks

VM disk encryption 

- Encryption at host `off`

OS disk

- OS disk size `image default (39GiB)`
- OS disk type `Standard SSD (locally-redundant storage)`
- delete with VM `yes`
- Key Management `Platform-managed key`
- Enable Ultra Disk compability `no`

## Networking

Network interface

- Virtual network `(new) test-vm-vnet`
- Subnet `(new) default (10.0.0.0/24)`
- Public IP `(new) test-vm-ip`
- NIC network security group `Basic`
- Public inbound ports `Allow selected ports`
- Select inbound ports `SSH (22)`
- Delete public IP and NIC when VM is deleted `yes`
- Enable accelerated networking `no`

Load balancing

- Load balancing options `None`

## Advanced

Userdata

```
#cloud-config

package_update: true

runcmd:
 - curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
 - apt install -y gitlab-runner
 - gitlab-runner register  --url https://gitlab.com  --token <runner-token> --name super-azure-runner --executor shell -n
```

# SSH into your virtual machine
```
ssh azureuser@0.0.0.0 -i ~/ssh/my_ssh_key
```
