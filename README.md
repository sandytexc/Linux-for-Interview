### Describe how you would secure SSH on a Linux server. 

Answer:
To secure SSH:
1. Disable root login by editing /etc/ssh/sshd_config:
2. PermitRootLogin no
3. Use key-based authentication instead of passwords.
4. Change the default SSH port from 22 to another number.
5. Implement fail2ban to block repeated failed login attempts.
6. Restrict SSH access to specific IP addresses.

#### Virtualization : 

This technology creates a virtual representation of server, storage and network. Virtualization is a process that allows a computer to share its hardware resources with multiple digitally separated environments. Each virtualized environment runs within its allocated resources, such as memory, processing power, and storage. Virtual software mimics the function of physical hardware to run multiple virtual machines simultaneously on a single physical machine.

#### Hypervisor: 

It is virtualization software that we can install on your physical machine. It creates a layer between the host machine(physical machine) and the virtual machine. The hypervisor coordinates access to the physical environment so that several virtual machines can access their share of physical resources.
 
Type of Hypervisor :
1. Type 1 Hypervisor or Bare Metal Hypervisor: Runs directly on the computer hardware.
2. Type 2 Hypervisor: Use this type of hypervisor when running multiple operating systems on a single machine. 

AWS: Uses Xen and Nitro hypervisors.
GCP: Uses KVM hypervisor.
Azure: Uses a customized version of Hyper-V.
