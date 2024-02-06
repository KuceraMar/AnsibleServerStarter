# Manual Configuration for Ansible

This guide provides step-by-step instructions for setting up Ansible manually on a clean Ubuntu 22 system.

## Preparation

Ensure you have a clean installation of the Ubuntu operating system or similar.

## Installation (On Control Server Only)

1. Update package lists: sudo apt update
2. Upgrade installed packages: sudo apt upgrade
3. Install Ansible on the control server: sudo apt install ansible
4. Verify Ansible installation: ansible --version

## Ansible Configuration on the Control Server

1. Create the Ansible configuration directory: mkdir /home/user/.ansible
2. Navigat to the Ansible directory: cd /home/user/.ansible
3. Create the "hosts" file: touch hosts
4. Create the "ansible.cfg" file: touch ansible
5. Generate an SSH key pair for Ansible: ssh-keygen -t rsa -b 4096 -C "email@email.cz" -f  ~/.ssh/ansible_rsa
6. Edit the "hosts" file: sudo nano hosts
7. Add the following content:
       all:
            hosts:
                server1:
                    ansible_host: 10.0.0.10
8. Edit the "ansible.cfd" file: sudo nano ansible.cfg
9. Add the following content: 
[defaults]
inventory = /home/user/.ansible/hosts
remote_user = root
private_key_file = /home/user/.ssh/ansible_rsa

[ssh_connection]
ssh_args = -o ServerAliveInterval=10

## Configuraton on Server
1. cp /home/user/.ssh/ansible_rsa.pub /home/user/.ssh/authorized_keys
Alternatively, you can use the following command for the same purpose:
1. ssh-copy-id -i ~/.ssh/ansible_rsa.pub user@server2

## Test
ssh -i /home/user/.ssh/ansible_rsa root@10.0.0.10


   

