# Day 33 - Azure Load Balancer

Created the `xfusion-lb` Standard Load Balancer in `eastus` with public IP `xfusion-lb-ip`, configured `xfusion-backend-pool` with `xfusion-vm`, added an HTTP health probe and port 80 load-balancing rule, allowed HTTP traffic through the VM NSG, and verified the public IP returned Nginx with HTTP 200.
