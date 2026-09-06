# Day 34 - Azure VM Connectivity Troubleshooting

* Investigated package installation failure on xfusion-vm.
* Verified VM, VNet, subnet, NIC, and public IP.
* Confirmed DNS and routing were configured correctly.
* Found Block-All-Outbound NSG rule at priority 200.
* Removed the blocking outbound rule from xfusion-nsg.
* Restored outbound internet connectivity for the VM.
* Verified apt update successfully downloaded package repositories.
* Installed curl successfully to confirm package installation works.
* Verified curl installation and functionality.
