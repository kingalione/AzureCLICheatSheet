### Create new VM:

```

New-AzVm -ResourceGroupName learn-f36664df-9d9c-480f-bdd4-5ee52398cf97 -Name "testvm-eus-01" -Credential (Get-Credential) -Location "eastus" -Image Canonical:0001-com-ubuntu-server-focal:20_04-lts:latest -OpenPorts 22 -PublicIpAddressName "testvm-eus-01"

```

### Assign VM to variable:

```

$vm = (Get-AzVM -Name "testvm-eus-01" -ResourceGroupName learn-f36664df-9d9c-480f-bdd4-5ee52398cf97)

```

### Get public IP of VM

```

Get-AzPublicIpAddress -ResourceGroupName learn-f36664df-9d9c-480f-bdd4-5ee52398cf97 -Name "testvm-eus-01"

```

### Connect to VM

```

ssh <username>@<ip-address>

```

### Stop the VM

```

Stop-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName

```

### Delete the VM

```

Remove-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName

```

### List all resources in resource group

```

Get-AzResource -ResourceGroupName $vm.ResourceGroupName | Format-Table

```

### Delete network interface

```

$vm | Remove-AzNetworkInterface –Force

```

### Delete managed OS disks

```

Get-AzDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzDisk -Force

```

### Delete virtual network

```

Get-AzVirtualNetwork -ResourceGroupName $vm.ResourceGroupName | Remove-AzVirtualNetwork -Force

```

### Delete network security group

```

Get-AzNetworkSecurityGroup -ResourceGroupName $vm.ResourceGroupName | Remove-AzNetworkSecurityGroup -Force

```

### Delete public ip address

```

Get-AzPublicIpAddress -ResourceGroupName $vm.ResourceGroupName | Remove-AzPublicIpAddress -Force

```