# Building a Kubernetes Cluster
This repository acts as a guide to build a Kubernetes Cluster of 3 nodes with Kubeadm.

![](images/kubernetes%20icon%201.png)


<h2> Attribution </h2>
Hello everyone, you are welcome to make use of this guide and learn from it but please do not copy without giving attribution to the author.

<h2> Let's Start the Guide </h2>
Kubernetes (K8s) is an open-source system for automating deployment, scaling, and management of containerized applications. It automates the application infrastructure and make it easy to manage it. Kubernetes is all about managing containers. Hope you know well about containers like what they are, how they are more efficient and faster than virtual machines. Go and have a look on the basics of containers before starting to build your K8s cluster.

Docker is the container runtime we will be using. A container runtime is the software that actually runs the containers. Kubernetes supports several other container runtimes such as rkt and containerd but Docker is the most popular.

The first step in building the cluster is to install Docker(container runtime) on 3 servers. You will be requiring 3 Ubuntu servers to build a Kubernetes cluster.
One server will act as a master node and other 2 servers as worker nodes.
First install Docker on master node.
<h3> Installing Docker </h3>
<h4>1. Add the Docker repository GPG key </h4>

```javascript
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
![](images/1.png)
<h4>2. Add the Docker repository </h4>

```javascript
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
![](images/2.png)
<h4> 3. Update the system </h4>
It is advisable to run this before installing any package and necessary to run it to install the latest updates.

```javascript
sudo apt-get update
```
![](images/3.png)
<h4> 4. Install Docker </h4>

```javascript
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu
```
![](images/4.png)
<h4> 5. Prevent auto-updates for the Docker package </h4>

```javascript
sudo apt-mark hold docker-ce
```
![](images/5.png)

Now, verify whether the Docker is working or not by running this command
```javascript
sudo docker version
```
![](images/6.png)

If you are able to see the above information after running <b>sudo docker version</b> command then you have successfully installed Docker on the master node and your Docker is up and running.

<b>Note:</b>
Repeat the same commands of installing Docker on both the worker nodes as you did on master node. After installing Docker on both the worker nodes, make sure to verify the docker is working or not. I am not showing here because it is the same process.

<h3> Installing Kubeadm, Kubelet, and Kubectl </h3>
Now that Docker is installed, we are ready to install the Kubernetes components.

* <b>Kubeadm</b> - This is a tool which automates a large portion of the process of setting up a cluster.

* <b>Kubelet</b> - The essential component of K8s that handles running containers on a node. Every server that will be running container needs kubelet.

* <b>Kubectl</b> - Command line tool for interacting with the cluster once it is up. kubectl is used to manage the cluster.

Let's install kubeadm, kubelet and kubectl on all three servers.
<h4> 1. Add the Kubernetes repository GPG key </h4>

```javascript
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```
![](images/7.png)
<h4> 2. Add the Kubernetes repository </h4>

```javascript
cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```
![](images/8.png)
<h4> 3. Update the system </h4>

```javascript
sudo apt-get update
```
![](images/9.png)
<h4> 4. Install Packages </h4>

```javascript
sudo apt-get install -y kubelet=1.12.7-00 kubeadm=1.12.7-00 kubectl=1.12.7-00
```
![](images/10.png)
<h4> 5. Prevent auto-updates for the Kube packages </h4>

```javascript
sudo apt-mark hold kubelet kubeadm kubectl
```
![](images/11.png)
After installing these components, verify that kubeadm is working properly. You can verify using

```javascript
kubeadm version
```
![](images/12.png)
