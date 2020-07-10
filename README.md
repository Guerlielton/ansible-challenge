**My reference guide**

<https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu>
<https://docs.ansible.com/ansible/latest/modules/list_of_cloud_modules.html>

**Setup GCP**

Create a new project

Add a new service account to the project on the IAM & admin => Service accounts tab. Click create add name service account,
grant permission to the 'compute admin'.

Create a private key the service account,on the IAM & admin => Service accounts tab. Click in create key choose the Json key type, download the private key json file, add place it in safe location acessible with ansilbe in modules next step

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

- google-auth required for work modules ansible gcp

- pip3 resquest, required for work dynamic inventory with ansible gcp

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

**I user sudo -s in next Step**

**Run Fist Playbook**

Navigate to your install ansible directory in my case located in, cd /etc/ansible/
create new file with code yaml with of this file the repository example:

```
cd /etc/ansible

# nano create-instance.yaml

```

**Atention in indention the code.**

Run playbook

```
# ansible-playbook create-instance

```

Get ip address gereneted in output command playbook add ip in file hosts.

```
    - name: Show Details Instance
      debug:
        msg: "The instance is accessible at {{ address.address }}"
```

My file hosts default

```
[web-server]
ip output above the command playbook

```

**Run Second Playbook**

Follow the previous step to create the file.

```
# nano install-docker.yaml

```

This playbook install the docker with pre-defined, access ssh in step **Setup GCP**
where pull image from docker hub and next run the container, my docker image contain node in version 10

```
# ansible-playbook install-docker.yaml

```

**Testing the application at the end**

```
curl [add you ip]
Welcome To The Challenge Devops ! %

```
