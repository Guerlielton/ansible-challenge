**Setup GCP**

Create a new project

Add a new service account to the project on the IAM & admin => Service accounts tab. Click create add name service account,
grant permission to the 'compute admin'

Create a private key the service account,on the IAM & admin => Service accounts tab. Click in create key choose the Json key type, Download the private key json file, add place it in safe location acessible with ansilbe in modules next step

Create a ssh public/private key pair will be used to access GCP Instance by ansible example:

```sh
ssh-keygen -t rsa -b 4096 -C "ansible"
cat ~/.ssh/ansible.pub

```

Copy new public key for into the metadata in GCP steep: Compute Engine => Metadata => SSH Keys => select add item,input the public key obtained by output comand cat

**Setup Ansible**

My setup use ubuntu 20.

```
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```

Your need install two extras package important in next step.

```
pip3 install requests google-auth
```

*google-auth required for work modules ansible gcp
*pip3 resquest, required for work dynamic inventory with ansible gcp

**Basic Ansible Configuration**

My directory ansible is located at cd /etc/ansible
edit the ansible.cfg using the text editor you prefer.

My values

```
[defaults]
# Bypass host key checking in Ansible
host_key_checking = False
# Path your file genereted in command ssh-keygen -t rsa -b 4096 -C "ansible"
private_key_file = /home/guerlielton/.ssh/ansible
# Remote user who will accesse the instance with public key
remote_user = ansible
# Path static inventory this moment in use
inventory = /etc/ansible/hosts

```
