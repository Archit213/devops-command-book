# Kubernetes & Minikube Setup Guide

A comprehensive guide and reference for installing `kubectl`, Minikube, and VirtualBox, along with a quick-start tutorial and macOS-specific tunneling instructions.

---

## Table of Contents
1. [Prerequisites & Tool Installation](#1-prerequisites--tool-installation)
   * [Install kubectl](#install-kubectl)
   * [Install Minikube](#install-minikube)
   * [Install VirtualBox](#install-virtualbox)
2. [Minikube Tutorial (Hello Minikube)](#2-minikube-tutorial-hello-minikube)
3. [macOS Troubleshooting: Accessing Services with Minikube Tunnel](#3-macos-troubleshooting-access-services-with-minikube-tunnel)

---

## 1. Prerequisites & Tool Installation

### Install kubectl
To interact with your Kubernetes clusters, install the official command-line tool:
* **Documentation & Instructions:** [Kubectl Installation Guide](https://kubernetes.io/docs/tasks/tools/)

### Install Minikube
Minikube runs a single-node Kubernetes cluster locally so you can test and develop applications:
* **Documentation & Instructions:** [Minikube Start Guide](https://minikube.sigs.k8s.io/docs/start/)

### Install VirtualBox
VirtualBox is commonly used as a local hypervisor driver for running Minikube VMs:
* **General Downloads:** [VirtualBox Downloads Page](https://www.virtualbox.org/wiki/Downloads)
* **Linux Specific:** [VirtualBox Linux Downloads](https://www.virtualbox.org/wiki/Linux_Downloads)

---

## 2. Minikube Tutorial (Hello Minikube)

Once your environment tools and hypervisor are configured, follow the official tutorial to deploy your first containerized application on your local cluster:
* **Tutorial Link:** [Hello Minikube Tutorial](https://kubernetes.io/docs/tutorials/hello-minikube/)

---

## 3. macOS Troubleshooting: Access Services with Minikube Tunnel

If you have installed and run Minikube on **macOS**, reaching your deployed services via a local browser requires an active network tunnel to expose NodePort services properly.

* **Detailed Documentation:** [Minikube Accessing Services Guide](https://minikube.sigs.k8s.io/docs/handbook/accessing/#using-minikube-service-with-tunnel)

### Quick Command Overview for macOS Tunneling:
1. Run the service tunnel command in a dedicated terminal window:
   ```bash
   minikube service <service-name> --url