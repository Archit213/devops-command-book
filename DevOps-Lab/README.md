# 🚀 Automated DevOps Lab: Ansible, Docker & Minikube on Vagrant with Nginx App Deployment

[![Vagrant](https://img.shields.io/badge/Vagrant-2.3%2B-blue?logo=vagrant&logoColor=white)](https://www.vagrantup.com/)
[![VirtualBox](https://img.shields.io/badge/VirtualBox-7.0%2B-orange?logo=virtualbox&logoColor=white)](https://www.virtualbox.org/)
[![Ansible](https://img.shields.io/badge/Ansible-2.14%2B-red?logo=ansible&logoColor=white)](https://www.ansible.com/)
[![Docker](https://img.shields.io/badge/Docker-CE-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Kubernetes/Minikube](https://img.shields.io/badge/Minikube-Kubernetes-326CE5?logo=kubernetes&logoColor=white)](https://minikube.sigs.k8s.io/)
[![Nginx](https://img.shields.io/badge/Nginx-Web_Server-009639?logo=nginx&logoColor=white)](https://nginx.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end Infrastructure-as-Code (IaC), Configuration Management, and Container Orchestration lab built for beginners. This project provisions two Ubuntu 22.04 virtual machines using **Vagrant** and **VirtualBox**, configures an **Ansible Control Node** to install **Docker**, **Kubectl**, and **Minikube** on a **Target Node**, and demonstrates deploying an **Nginx Web Application** on the local Kubernetes cluster.

---

## 📑 Table of Contents

- [Architecture Overview](#-architecture-overview)
- [Lab Specifications](#-lab-specifications)
- [Directory Structure](#-directory-structure)
- [Prerequisites](#-prerequisites)
- [Step-by-Step Implementation Guide](#-step-by-step-implementation-guide)
  - [Step 1: Configure & Boot Virtual Machines](#step-1-configure--boot-virtual-machines)
  - [Step 2: Connect to VMs via SSH](#step-2-connect-to-vms-via-ssh)
  - [Step 3: Setup Passwordless SSH (Controller -> Target)](#step-3-setup-passwordless-ssh-controller---target)
  - [Step 4: Install Ansible on Controller](#step-4-install-ansible-on-controller)
  - [Step 5: Write Inventory & Playbook](#step-5-write-inventory--playbook)
  - [Step 6: Execute Playbook on Controller](#step-6-execute-playbook-on-controller)
  - [Step 7: Launch Minikube Cluster on Target Node](#step-7-launch-minikube-cluster-on-target-node)
  - [Step 8: Deploy & Test Nginx Application](#step-8-deploy--test-nginx-application)
- [Troubleshooting & Common Fixes](#-troubleshooting--common-fixes)
- [Teardown & Cleanup](#-teardown--cleanup)
- [License](#-license)

---

## 🏗️ Architecture Overview

```
+---------------------------------------------------------------------------------------+
|                            HOST MACHINE (Windows / macOS / Linux)                     |
|                                                                                       |
|  +---------------------------------------------------------------------------------+  |
|  |                 Terminal / PowerShell / MobaXterm (SSH Access)                  |  |
|  +---------------------------------------------------------------------------------+  |
|                          |                                    |                       |
|       (vagrant ssh / :22)|                 (vagrant ssh / :22)|                       |
|                          v                                    v                       |
|  +---------------------------------------------------------------------------------+  |
|  |                              ORACLE VIRTUALBOX                                  |  |
|  |                                                                                 |  |
|  |   +-----------------------------+         +---------------------------------+   |  |
|  |   |     Ansible Controller      |         |           Target Node           |   |  |
|  |   |     IP: 192.168.56.10       |         |        IP: 192.168.56.20        |   |  |
|  |   |     OS: Ubuntu 22.04 LTS    |         |        OS: Ubuntu 22.04 LTS     |   |  |
|  |   |     RAM: 2GB | vCPU: 2      |         |        RAM: 4GB | vCPU: 2       |   |  |
|  |   |                             | Ansible |                                 |   |  |
|  |   |   • Ansible Core Engine     | SSH     |   • Docker CE Engine            |   |  |
|  |   |   • Playbooks & Inventory   |-------->|   • Minikube Single-Node Cluster|   |  |
|  |   |   • SSH Key Management      |  (Port  |   • Kubectl CLI Tool            |   |  |
|  |   |                             |   22)   |   • [App] Nginx Deployment & Svc|   |  |
|  |   +-----------------------------+         +---------------------------------+   |  |
|  +---------------------------------------------------------------------------------+  |
+---------------------------------------------------------------------------------------+
```

---

## 🖥️ Lab Specifications

| Node Name | Hostname | IP Address | vCPU | RAM | Operating System | Purpose / Components |
| :--- | :--- | :--- | :---: | :---: | :--- | :--- |
| **Controller** | `ansible-controller` | `192.168.56.10` | 2 | 2048 MB | Ubuntu 22.04 LTS | Ansible Engine, Orchestration |
| **Target Node**| `target-node` | `192.168.56.20` | 2 | 4096 MB | Ubuntu 22.04 LTS | Docker Engine, Minikube, Kubectl, Nginx App |

---

## 📂 Directory Structure

```text
.
├── Vagrantfile                         # Infrastructure-as-Code for VirtualBox VMs
├── README.md                           # Complete walkthrough documentation
└── ansible/
    ├── hosts.ini                       # Inventory defining target node IP & credentials
    ├── setup-docker-minikube.yml       # Configuration playbook for software stack
    └── nginx-k8s-deploy.yml            # (Optional) Playbook for automated Nginx deploy
```

---

## ⚙️ Prerequisites

Install the following tools on your host workstation:

1. **[Oracle VM VirtualBox](https://www.virtualbox.org/)** (v7.0+)
2. **[Vagrant](https://developer.hashicorp.com/vagrant/downloads)** (v2.3+)
3. **Any Terminal / SSH Client**:
   - **Windows:** PowerShell / Windows Terminal
   - **macOS / Linux:** Native Terminal

> **Note:** Restart your host system after installing VirtualBox and Vagrant to ensure virtualization network drivers are loaded.

---

## 🚀 Step-by-Step Implementation Guide

### Step 1: Configure & Boot Virtual Machines

1. Create a project directory on your host machine (e.g., `D:\DevOps-Lab` or `~/DevOps-Lab`).
2. Create a file named `Vagrantfile` with the following configuration:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  # 1. Ansible Controller Node
  config.vm.define "ansible-controller" do |node|
    node.vm.hostname = "ansible-controller"
    node.vm.network "private_network", ip: "192.168.56.10"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "ansible-controller"
      vb.memory = "2048"
      vb.cpus = 2
      vb.linked_clone = true
    end
  end

  # 2. Target Server
  config.vm.define "target-node" do |node|
    node.vm.hostname = "target-node"
    node.vm.network "private_network", ip: "192.168.56.20"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "target-node"
      vb.memory = "4096"
      vb.cpus = 2
      vb.linked_clone = true
      vb.customize ["modifyvm", :id, "--nested-hw-virt", "on"]
    end
  end
end
```

3. Launch both virtual machines:
   ```bash
   vagrant up
   ```

4. Verify status:
   ```bash
   vagrant status
   ```
   *Both machines should display `running (virtualbox)`.*

---

### Step 2: Connect to VMs via SSH

Open **two separate terminal windows** on your host:

#### Window 1: Connect to Controller
```bash
vagrant ssh ansible-controller
```

#### Window 2: Connect to Target Node
```bash
vagrant ssh target-node
```

---

### Step 3: Setup Passwordless SSH (Controller -> Target)

#### 1. On `target-node` (Window 2):
Ensure password authentication is enabled for initial key exchange:
```bash
sudo sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
sudo sed -i 's/^KbdInteractiveAuthentication no/KbdInteractiveAuthentication yes/' /etc/ssh/sshd_config
sudo sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config.d/*.conf 2>/dev/null || true
sudo systemctl restart ssh
echo "vagrant:vagrant" | sudo chpasswd
```

#### 2. On `ansible-controller` (Window 1):
Generate an SSH key and copy it to the target:
```bash
# Generate SSH key pair
ssh-keygen -t rsa -b 2048 -N "" -f ~/.ssh/id_rsa

# Copy public key to target node (Password: vagrant)
ssh-copy-id vagrant@192.168.56.20
```

Verify passwordless connection:
```bash
ssh vagrant@192.168.56.20
```
*(If you enter without a password prompt, type `exit` to return to `ansible-controller`).*

---

### Step 4: Install Ansible on Controller

Inside the **`ansible-controller`** terminal (Window 1):

```bash
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install -y ansible
```

---

### Step 5: Write Inventory & Playbook

Inside **`ansible-controller`** (Window 1):

1. Create a project directory:
   ```bash
   mkdir -p ~/ansible-project
   cd ~/ansible-project
   ```

2. Create `hosts.ini`:
   ```bash
   cat << 'EOF' > hosts.ini
   [targets]
   target-node ansible_host=192.168.56.20 ansible_user=vagrant
   EOF
   ```

3. Test Ansible connection:
   ```bash
   ansible targets -i hosts.ini -m ping
   ```
   *Expected Output: `"ping": "pong"` (SUCCESS)*.

4. Create the playbook `setup-docker-minikube.yml`:
   ```bash
   cat << 'EOF' > setup-docker-minikube.yml
   ---
   - name: Install Docker, Kubectl, and Minikube on Target Node
     hosts: targets
     become: yes
     tasks:

       - name: Update apt cache
         apt:
           update_cache: yes
           cache_valid_time: 3600

       - name: Install prerequisite packages
         apt:
           name:
             - apt-transport-https
             - ca-certificates
             - curl
             - gnupg
             - lsb-release
             - conntrack
           state: present

       - name: Install Docker Engine
         apt:
           name: docker.io
           state: latest

       - name: Ensure Docker is started and enabled
         systemd:
           name: docker
           state: started
           enabled: yes

       - name: Add 'vagrant' user to docker group
         user:
           name: vagrant
           groups: docker
           append: yes

       - name: Download and install Minikube binary
         get_url:
           url: https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
           dest: /usr/local/bin/minikube
           mode: '0755'

       - name: Download and install Kubectl binary
         get_url:
           url: "https://dl.k8s.io/release/v1.30.0/bin/linux/amd64/kubectl"
           dest: /usr/local/bin/kubectl
           mode: '0755'
   ```

---

### Step 6: Execute Playbook on Controller

Run the playbook from `ansible-controller`:

```bash
ansible-playbook -i hosts.ini setup-docker-minikube.yml
```

Ansible will execute each task idempotently and output a green/yellow `PLAY RECAP`.

---

### Step 7: Launch Minikube Cluster on Target Node

Switch to **Window 2 (`target-node`)**:

1. Refresh user group permissions (or reconnect via `vagrant ssh target-node`):
   ```bash
   newgrp docker
   ```

2. Verify Docker and Kubectl:
   ```bash
   docker ps
   kubectl version --client
   ```

3. Start your single-node Minikube cluster:
   ```bash
   minikube start --driver=docker
   ```

4. Verify cluster health:
   ```bash
   minikube status
   kubectl get nodes
   ```
   *Expected Output: `minikube` node listed with status `Ready`.*

---

### Step 8: Deploy & Test Nginx Application

Inside the **`target-node`** (Window 2):

1. **Deploy an Nginx instance with 2 replicas:**
   ```bash
   kubectl create deployment nginx-web --image=nginx --replicas=2
   ```

2. **Verify Pods are running:**
   ```bash
   kubectl get pods -o wide
   ```

3. **Expose the deployment via a NodePort Service:**
   ```bash
   kubectl expose deployment nginx-web --type=NodePort --port=80
   ```

4. **Verify Service & assigned NodePort:**
   ```bash
   kubectl get svc nginx-web
   ```

5. **Test web connectivity to Nginx:**
   ```bash
   # Retrieve the cluster-accessible service URL
   minikube service nginx-web --url
   ```
   Or send a direct HTTP request:
   ```bash
   curl $(minikube service nginx-web --url)
   ```
   *You will see the default `<h1>Welcome to nginx!</h1>` HTML response.*

---

## 🔧 Troubleshooting & Common Fixes

| Problem | Cause | Solution |
| :--- | :--- | :--- |
| **`Permission denied (publickey)`** | SSH password auth is disabled on target node by default. | Run the `sshd_config` update commands in Step 3 on `target-node`. |
| **`permission denied unix:///var/run/docker.sock`** | User group permissions have not reloaded. | Run `newgrp docker` or reconnect via `vagrant ssh target-node`. |
| **`EOF / Syntax Error in YAML`** | Extra EOF delimiters copied into playbook file. | Re-write the file using the quoted `cat << 'EOF'` commands. |
| **`Minikube: VT-x/AMD-V virtualization is not enabled`** | Nested virtualization disabled. | Ensure `vb.customize ["modifyvm", :id, "--nested-hw-virt", "on"]` is in `Vagrantfile`. |

---

## 🧹 Teardown & Cleanup

Manage the lab lifecycle from your host terminal:

* **Suspend virtual machines:**
  ```bash
  vagrant halt
  ```
* **Resume virtual machines:**
  ```bash
  vagrant up
  ```
* **Destroy VMs and release disk space:**
  ```bash
  vagrant destroy -f
  ```

---

## 📜 License
This project is open-source and released under the [MIT License](LICENSE).
