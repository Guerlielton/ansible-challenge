Create a ssh public/private key pair will be used to access GCP Instance by ansible example

```sh
ssh-keygen -t rsa -b 4096 -C "ansible"
cat ~/.ssh/ansible.pub

```

Copy new public key for into the metadata in GCP steep: Compute Engine => Metadata => SSH Keys => select add item,input the public key obtained by output comand cat

**Setup Ansible**
My setup use ubuntu 20.

- sudo apt-add-repository ppa:ansible/ansible
- sudo apt update
- sudo apt install ansible

Your need install two extras package important in next step.

- pip3 install requests google-auth
- Google auth requred for work modules ansible gcp
- pip3 resquest, required for work dynamic inventory with ansible gcp

**Basic Ansible Configuration**
My directory ansible is located at cd /etc/ansible
edit the ansible.cfg using the text editor you prefer.
My values

**[defaults]**

- host_key_checking = False
- private_key_file = /home/guerlielton/.ssh/ansible
- remote_user = ansible
- inventory = /etc/ansible/hosts
