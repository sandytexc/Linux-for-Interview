### Question 1: Describe how you would secure SSH on a Linux server. 

Answer:
To secure SSH:
1. Disable root login by editing /etc/ssh/sshd_config:
2. PermitRootLogin no
3. Use key-based authentication instead of passwords.
4. Change the default SSH port from 22 to another number.
5. Implement fail2ban to block repeated failed login attempts.
6. Restrict SSH access to specific IP addresses.
