![](https://github.com/microsoft/sqlworkshops/blob/master/graphics/microsoftlogo.png?raw=true)

# Workshop: Kubernetes - From Bare Metal to SQL Server Big Data Clusters

#### <i>A Microsoft Course from the SQL Server team</i>

<p style="border-bottom: 1px solid lightgrey;"></p>

<h2><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/textbubble.png?raw=true"> 03 - Kubernetes Concepts and Implementation </h2>

In this workshop you have covered the hardware and software environment for Kubernetes. You've learned about Linux, Containers, and a quick overview of Kubernetes. With all that in place, in the previous Module you set up your environment to install Kubernetes. We didn't cover the terms you used to define and deploy your cluster.  
This module covers the concepts, terms, and tools for Kubernetes. You'll follow various exercises to ground your understanding of each topic, and the end of this Module contains several helpful references you can use in these exercises and in production.

We'll begin with a set of definitions. These aren't all the terms used in Kubernetes - you'll see more as you work through the Modules - but they do form the basics for the concepts that follow. You'll work with each of these terms throughout this Module and the rest of the course, so just familiarize yourself with them, and refer back to this list as you work through each section. 

<table style="tr:nth-child(even) {background-color: #dddddd;}; text-align: left; display: table; border-collapse: collapse; border-spacing: 5px; border-color: gray; ">
	<tbody>
		<tr style="vertical-align:top;">
			<th>Category </th>
			<th>Term </th>
			<th>Description </th>
		</tr>
		<tr style="vertical-align:top;">
			<td><a href="https://kubernetes.io/docs/reference/tools/"><b>Tools</b></a> </td>
			<td><a href="https://kubernetes.io/docs/concepts/overview/kubernetes-api/"><i>The Kubernetes API</i></a> </td>
			<td>The foundation for the declarative configuration schema calls for the entire system. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/reference/kubectl/overview/"><i>kubectl</i></a> </td>
			<td>A command-line control tool for a Kubernetes cluster. Used from a client workstation or a "Jump Box" that acts as the client for your environment. This tool can be installed on Windows, Linux and Mac OS/X. Uses a set of configurations set in a text file to connect to a Kubernetes cluster. </td>
        </tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/reference/tools/#kubeadm"><i>kubeadm</i></a> </td>
			<td>A command-line tool for easily provisioning a secure Kubernetes cluster on top of physical or cloud servers or virtual machines. </td>
        </tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/reference/tools/#dashboard"><i>The Kubernetes Dashboard</i></a> </td>
			<td>A web-based Kubernetes interface that allows you to deploy containerized applications to a Kubernetes cluster, troubleshoot them, and manage the cluster and its resources. </td>
        </tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://github.com/etcd-io/etcd/tree/master/etcdctl"><i>etcdctl</i></a> </td>
			<td>etcdctl command line tool.</td>
        </tr>
		<tr style="vertical-align:top;">
			<td><a href="https://kubernetes.io/docs/concepts/"><b>Concepts</b></a> </td>
			<td><a href="https://kubernetes.io/docs/tasks/manage-kubernetes-objects/declarative-config/"><i>Declaritive API</i></a> </td>
			<td>Objects are specified according to the desired state that an object should be instantiated in. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/cluster-administration/networking/"><i>Overlay network</i></a> </td>
			<td>A software defined network via which nodes in the cluster communicate, this is usually implemented via a Container Network Interface compliant plugin, the default of which is Calico. </td>
        </tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/services-networking/ingress/"><i>Ingress</i></a> </td>
			<td>Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource. </td>
        </tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://github.com/container-storage-interface/spec/blob/master/spec.md">Persistent Storage </i></a> </td>
			<td>A hardware and software combination used to persist state. One of the key aims is ensure that if a Pod is rescheduled to run on a different Node, its state is not lost as it moves from its original Node to a new one. In the early days of Kubernetes, most storage drivers were called as “In tree”, meaning that vendors who wanted Kubernetes to use their storage had to integrate the code for their drivers directly with the Kubernetes code base. The IT industry is now gravitating towards the Container Storage Interface specification which allows Kubernetes to seamlessly use any storage platform that supports this standard without having to touch the Kubernetes code base. Ultimately, the aim of the CSI standard is to promote storage portability. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/">Bin packing</i></a> </td>
			<td>The algorithm by which pods are assigned to nodes based on each node's CPU and memory requirements and the available resouirces on each node.</td>
        </tr>
		<tr style="vertical-align:top;">
			<td><b><a href="https://kubernetes.io/docs/concepts/#kubernetes-objects">Object</b></a> </td>
			<td><a href="https://www.tutorialspoint.com/kubernetes/kubernetes_node.htm"><i>Node</i></a> </td>
			<td>The computers (physical or virtual) that host the rest of the Objects in a Kubernetes cluster. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/admin/kubelet/"><i>kubelet</i></a> </td>
			<td>Runs on each Node, and provides communication with the Kubernetes Master. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/admin/kube-proxy/"><i>kube-proxy </i></a> </td>
			<td>Runs on each Node, and provides a network proxy which reflects Kubernetes networking services. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/">Pod</i></a> </td>
			<td>The basic execution unit of a Kubernetes application - holds a processes running on your Cluster. It contains one or more <i>Containers</i>, the storage resources, a unique network IP, and any Container configurations. While the <i>docker daemon</i> is the most common container runtime used in a Kubernetes Pod, other container runtimes are also supported. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://kubernetes.io/docs/concepts/services-networking/service/">Service</i></a> </td>
			<td>A "description" of a set of Pods and a policy to access them. This de-couples the call to an application to it's physical representation, and allows the application running on the Pod to be more stateless. </td>
		</tr>	
    <tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/storage/volumes/"><i>Volume</i></a> </td>
			<td>A pointer to a storage directory - either "ethereal" (has the same lifetime as the Pod) or permanent. Can use various providers such as cloud storage and on-premises devices, and is set with various parameters. </td>
		</tr>
    <tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/storage/volumes/"><i>Persistent Volume</i></a> </td>
			<td>A piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes.</td>
		</tr>
    <tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/storage/volumes/"><i>Persistent Volume Claim</i></a> </td>
			<td>A request for storage from a PersistentVolume by a user.</td>
		</tr>
    <tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/storage/volumes/"><i>StorageClass</i></a> </td>
			<td>A StorageClass provides a way for administrators to describe the “classes” of storage available to a Kubenetes cluster.</td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/"><i>Namespace</i></a> </td>
			<td>Used to define multiple virtual clusters backed by the same physical cluster. Namespaces are a critical component in the Kubernetes role based access control security model.</td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/">Label</i></a> </td>
			<td>key/value pairs that are attached to objects, such as pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system.</td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/">Selector</i></a> </td>
			<td>Mechanism by which a client/user can identify a set of objects that have specific label(s).</td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/">Secret</i></a> </td>
			<td>An object that contains a small amount of sensitive data such as a password, a token, or a key.</td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><i><a href="https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/">ConfigMap</i></a> </td>
			<td>A resource for injecting containers with configuration data that allows containers to be Kubernetes agnostic.</td>
		</tr>
		<tr style="vertical-align:top;">
			<td><a href="https://kubernetes.io/docs/concepts/architecture/master-node-communication/"><b>Kubernetes Master</b></a> </td>
			<td><a href="https://kubernetes.io/docs/admin/kube-apiserver/"><i>kube-apiserver </i></a> </td>
			<td>Responds to REST calls to provide the frontend to the cluster’s shared state. This allows all commands through which all other components interact. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/reference/command-line-tools-reference/kube-controller-manager/"><i>kube-controller-manager</i></a> </td>
			<td>A daemon that embeds the non-terminating control loops shipped with Kubernetes that watches the shared state of the cluster through the API Server and makes changes to change the current state of the cluster to the desired state. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/"><i>kube-scheduler </i></a> </td>
			<td>A policy-driven scheduling service that is topology aware and specific to a workload. It is called for functions such as availability, performance, and capacity. </td>
		</tr>		
        <tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/cluster-administration/networking/"><i>Container Network Interface </i></a> </td>
			<td>The Nodes in the cluster communicate with each other via what is known as an <i>overlay network</i> - a software-defined network. There are a variety of CNI plugins that Kubernetes can use. This Workshop uses the the default <i>Calico</i> CNI plugin. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/security/overview/"><i>Certificate Management </i></a> </td>
			<td>Security management for a Kubernetes cluster is managed through <a href="https://kubernetes.io/docs/concepts/configuration/secret/">Secrets which can use Certificates</a>. This concept deals with those layers. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://metallb.universe.tf/"><i>Ingress Management (Optional) </i></a> </td>
			<td>A key difference between "Vanilla" Kubernetes and an Kubernetes-As-A-Service (such as Azure Kubernetes Service) is that services do not come with load balancing endpoints by default. Load balancer services for Kubernetes on-premises is enabled using a compenent that carries out ingress management.</td>
		</tr>
		<tr style="vertical-align:top;">
			<td><a href="https://kubernetes.io/docs/concepts/architecture/cloud-controller/"><b>Control </b></a> </td>
			<td><a href="https://kubernetes.io/docs/concepts/architecture/controller/"><i>Controller</i></a> </td>
			<td>A "plugin" mechanism that allows cloud providers to integrate with Kubernetes easily. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/workloads/controllers/deployment/"><i>Deployment</i></a> </td>
			<td>A YAML file describing the state of Pods and ReplicaSets. Deployed to the <i>Kubernetes API</i> using <i>kubectl</i> or <i>REST</i> calls. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/"><i>DaemonSet</i></a> </td>
			<td>A service that ensures that <i>Nodes</i> run a copy of a <i>Pod</i>. As Nodes are added to the cluster, Pods are added to them. As Nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a hrf="https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/"><i>StatefulSet</i></a> </td>
			<td>The workload API object used to manage stateful applications that are clustered by nature. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/"><i>ReplicaSet </i></a> </td>
			<td>A service that maintains a stable set of replica Pods running at any given time. Used to guarantee the availability of a specified number of identical Pods. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/"><i>Job</i></a> </td>
			<td>A Job creates one or more Pods and ensures that a specified number of them successfully terminate. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/#kubernetes-control-plane"><i>Control Plane</i></a> </td>
			<td>Contains components such as the <i>Kubernetes Master</i> and <i>kubelet</i> processes that governs how Kubernetes communicates with your cluster. The Control Plane maintains a record of all of the Kubernetes Objects in the system, and runs continuous control loops to manage those objects’ state. At any given time, the Control Plane’s control loops will respond to changes in the cluster and work to make the actual state of all the objects in the system match the desired state that you provided. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/"><i>etcd</i></a> </td>
			<td>A high performance key value store that stores the cluster’s state. Since <i>etcd</i> is  light-weight, each instance can generally share resources with other Nodes in the cluster. The Hardware recommendations section of the official http://etcd.io site provides a detailed breakdown of the hardware requirement for <i>etcd</i>. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/extend-kubernetes/operator/"><i>operator</i></a> </td>
			<td>A custom Kubernetes object implemented for the management of applications with complex life cycles. </td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/"><i>Node Affinity </i></a> </td>
			<td>A property of pods that attracts them to a set of nodes (either as a preference or a hard requirement).</td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/"><i>Taint</i></a> </td>
			<td>A property that repels pods from particular nodes.</td>
		</tr>
		<tr style="vertical-align:top;">
			<td> </td>
			<td><a href="https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/"><i>Toleration</i></a> </td>
			<td>A property that allows pods to be scheduled on nodes with taints, something you might want to do with daemonsets for example.</td>
		</tr>
	</tbody>
</table>

<p style="border-bottom: 1px solid lightgrey;"></p>

<h2><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/pencil2.png?raw=true">3.1 Kubernetes Interfaces</h2>

"North-south" traffic between a Kubernetes cluster and the outside is made via the Kubernetes API server. There are a number of standard client tools for administering and utilising a Kubernetes cluster: 

**[kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)**
A command line tool for administering a Kubernetes cluster and creating / modifying Kubernetes objects via YAML files.

**[Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)**
A general purpose web based grpahical interface for Kubernetes.

**[Helm](https://helm.sh/)**
A tool for Kubernetes application package management and deployment.

Language Client Libraries
Client libraries exist for most of the popular third generation languages, such as [Python](https://github.com/kubernetes-client/python).

<p style="border-bottom: 1px solid lightgrey;"></p>

<h2><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/pencil2.png?raw=true">3.2 Deploying a Cluster</h2>

### 3.2.1 Control Plane ###

Provision must be made for the control plane to be highly available, this includes:

- The API server

- Master nodes

- etcd instance

It is recommended that a production grade cluster has a minimum of two master nodes and three etcd instances.

The standard method for bootstrapping the control plane in is use ```kubeadm init```.

### 3.2.2 Worker Nodes ###

A production grade SQL Server 2019 Big Data Cluster requires a minimum of three nodes each with 64 GB of RAM and 8 logical processors. The standard method for bootstrapping worker nodes and joining them to the cluster is to use ```kubeadm join```.

Consideration needs to be made for upgrading a Kubernetes cluster from one version to another and allowing the cluster to tolerate node failure(s). There are two options:

- **Upgrade each node in the cluster in-situ**

  This requires that a ‘Taint’ is applied to a node so that it cannot accept pods, the node is then drained of its current pod workload after which it can be upgraded. When the node is drained, the pods that are running on it need somewhere else to go, therefore this approach mandates that there are N+1 worker nodes (assuming one node is upgraded at a time). This approach runs the risk that if the upgrade fails for any reason, the cluster may be left in a state with worker nodes on different versions of Kubernetes.

- **Create a new cluster**

  Create a new cluster, deploy a big data cluster to it and then restore a backup of the data from the original cluster. This approach requires more hardware than the in-situ upgrade method. If the upgrade spans multiple versions of Kubernetes, for example the upgrade is from version 1.15 to 1.17, this method allows a 1.17 cluster to be created from scratch cleanly and then the data from 1.15 cluster restored onto the new 1.17 cluster.

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Create A Single Node Sandbox Environment</b></p>

In the previous section we looked at the workshop sandbox environments from an infrastructure perpsective, in this activity we will deploy a single node Kubernetes cluster (and SQL Server 2019 big data cluster) on the workshop virtual machines. This activity will result in the following components being installed on your Ubuntu virtual machine:

- A single node Kubernetes cluster
- kubectl
- Helm
- The Kubernetes dashboard
- local-storage storage class
- A single node SQL Server 2019 big data cluster
- azdata

<p><img style="margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/checkmark.png?raw=true"><b>Steps</b></p>

1. Log onto the your workshop virtual machine using a ssh client, your workshop leaders will provide you with an ip address, username and password. macOS users may use the ssh client already built into their operating system, windows users can use either [putty](https://www.putty.org/) or a DOS command shell.

2. Download the deployment script using this command:
```
curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
```
3. Set the permissions on this file such that it can be executed:
```
chmod +x setup-bdc.sh
```
4. Execute the cluster creation script as follows:
```
sudo ./setup-bdc.sh
```
5. Now that your single node cluster is up and running, list some of the key processes that your sandbox Kubernetes cluster consists of:
```
ps -ef | egrep'(containerd|docker|etcd|kubelet)'
```
6. List the log files for the pods that form your sandbox big data cluster:
```
ls -l /var/log/pods
```
7. Observe live process stats that include those of the comnponents that make up the sandbox Kubernetes cluster:
```
top
```

### 3.2.3 Kubernetes Production Grade Deployments ###

The environments used for the workshop hands on activities are created via a single script that leverages Kubeadm. Consider what a production deployments of a Kubernetes cluster might require:

- Deployment of multi-node clusters.

- Repeatable cluster deployments for different environments with minimal scripting and manual command entry.

Also consider the number of steps required to deploy a cluster using kubeadm:

- Import the keys and register the repository for Kubernetes on each machine that will host a cluster node.

- Configure docker and Kubernetes prerequisites on each machine.

- Configure docker and Kubernetes prerequisites on each machine.

- Create a YAML file in order to enable RBAC for the cluster

- Initialise the Kubernetes master on this machine.

- Boostrap each work node and join it to the cluster.

- Configure an agent / kubelet on each worker node.

Can this process be automated ?.

### 3.2.4 Introducing Kubespray ###

[Kubespray](https://kubespray.io/#/) is a Kubernetes cluster life cycle management tool based on Ansible playbooks, it can:

- Create clusters

- Upgrade clusters

- Remove clusters

- Add nodes to existing clusters

Kubespray is a Cloud Native Computing Foundation project and with its own [GitHub repository](https://github.com/kubernetes-sigs/kubespray).

### 3.2.4.1 An Overview of Ansible ###

Ansible is an open source declarative tool for deploying applications and infrastructure-as-code. Components of an application or infrastructure are specified declaratively in ‘Runbooks’. Unlike other infrastructure-as-code tools, Ansible does not require that a special node is built for the purpose of deploying applications and infrastructure. All that is required is a host on which Ansible can be installed. Files known as inventory files are used to specify Ansible deployment targets. In the case of Kubespray, the deployment targets are the hosts which nodes and etcd instances are to be created on. Communication between Ansible and the deployment targets specified in an inventory file is via ssh.

### 3.2.4.2 Prerequisites ###

In order to carry out the deployment of the Kubernetes cluster, a basic understanding of the following tasks is required:

- Ubuntu base operating system installation

- Ubuntu package management via apt

- Cloning a GitHub repo

- Setting up remote access to Ubuntu hosts with ssh

- Basic Ubuntu firewall configuration

### 3.2.4.3 Kubespray Workflow ###

Unlike other available deployment tools, Kubespray does everything for you in “One shot”. For example, Kubeadm requires that certificates on nodes are created manually, Kubespray not only leverages Kubeadm but it also looks after everything including certificate creation for you. Kubespray works against most of the popular public cloud providers and has been tested for the deployment of clusters with thousands of nodes. The real elegance of Kubespray is the reuse it promotes. If an organization has a requirement to deploy multiple clusters, once Kubespray is setup, for every new cluster that needs to be created, the only prerequisite is to create a new inventory file for the nodes the new cluster will use.
3.2.5 High Level Kubespray Workflow

The deployment of a Kubernetes cluster via Kubespray follows this workflow:

- Preinstall step

- Install Container Engine

- Install etcd

- Setup certificates

- Install Kubernetes master(s)

- Install Kubernetes worker(s)

- Configure network plugin

- Configure any add-ons

Conceptually the creation of a three-worker node cluster looks like this:

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_2_7_kubespray-flow.png?raw=true">

Note:
- The deployment is instigated from the jump server,
- The etcd instances can share nodes with the two masters and a worker node due to their minimal CPU and memory requirements,
- hosts.yaml contains the IP addresses of the hosts that the masters, etcd instances and workers will be deployed to,
- cluster.yml contains the play book for creating the Kubernetes cluster itself,
- The entire cluster is deployed via a single invocation of the ansible-playbook command.

### 3.2.5 Post Cluster Deployment Activities ###

Install kubectl - the primary tool for administering a Kubernetes cluster. kubectl requires a configuration file in order to access the cluster, by default kubectl will look for a file named config in the .kube directory under the home directory of the user that is logged in:

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_2_9_kubectl.png?raw=true">

The config file specifies clusters, users and contexts, a context being a label for connection details for a cluster in terms of a user and namespace. If kubectl cannot find a config file or it has been corrupted in any way when an attempt is made to run a command against a cluster, the following error message will appear:

**The connection to the server localhost:8080 was refused - did you specify the right host or port?**

The [Kubernetes documentation](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/) goes into detail regarding the creation of config files and contexts for accessing multiple clusters. The fastest and simplest way to create a config file is to copy the file: /etc/kubernetes/admin.conf off one of the master node hosts and onto the client machine that kubectl is installed on.

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Kubectl Familiarisation</b></p>
Now that your sandbox enivornment is up and running, its time to look at kubectl; the primary command line tool for managing and administering Kubernetes clusters. Use the [kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) for assistance with this activity.

<p><img style="margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/checkmark.png?raw=true"><b>Steps</b></p>

1. Display the config containing the context for accessing the sandbox Kubernetes cluster (hint: config switch).

2. Use kubectl to obtain the state of the cluster's single node, do this such that the operating system the node is running on is displayed (hint: use the -o switch)

3. Obtained detailed information on the sandbox cluster's single node using describe and make a note of the taint associated with the node (hint: kubectl describe).

4. All objects that live in a Kubernetes cluster reside in a namespace, when a big data cluster is created, all its objects reside in a namespace dedicated to that big data cluster. Use kubectl to obtain the names of namespaces present in the workshop cluster (hint: kubectl get)

<p style="border-bottom: 1px solid lightgrey;"></p>

## 3.2.6 Application Deployment (Package Management) ## 

The deployment of non-trivial applications often comes with following requirements:

- The ability to package components together.
- Version control.
- The ability to downgrade and upgrade packaged applications.

The use of YAML files does not meet the requirements of deploying complex applications, a problem exacerbated by trhe rise of microservice based architectures.

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_2_10_package_mgmt.PNG?raw=true">

Kubernetes solves this problem via [Helm](https://helm.sh/). Helm packages are defined in what are called charts, and charts in turn are stored in chart repositories. Whilst Helm is not required for deploying a SQL Server 2019 big data cluster, the chances are that there are supporting objects in the rest of your Kubernetes eco-system that require the use of Helm.

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Using Helm</b></p>
In this activity we will deploy a storage plugin using Helm, this activity will demonstrate:

- How to add a repository to your chart "Search space".
- The dry-run facility that Helm provides
- Specifying values for use with Helm
- Installing a software component using Helm

<p><img style="margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/checkmark.png?raw=true"><b>Steps</b></p>

Follow the steps in section 2.4.

## 3.3 OpenShift Container Platform ##

OpenShift Container Platform is a 100% Kubernetes compatible Platform-As-A-Service based on Kubernetes from Red Hat Software:

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_3_1_openshift.PNG?raw=true">

## 3.3.1 The Requirment For Commercially Supported Distributions of Kubernetes ##

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Understanding what open-source means</b></p>

<p><img style="margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/checkmark.png?raw=true"><b>Steps</b></p>

1. Use a search engine lookup the Kubernetes repository on GitHub.

2. Make a note of the licence that the Kubernetes project is available under.

3. On the GitHub page for the Kubernetes repository, click on 'Issues' (top left of the page), then by clicking on 'Sort', sort the issues in ascending date order. Note the age and severity of some of the issues.

4. Note the GitHub login of the individual who has raised issue #489.

5. In a browser navigate to the link https://landscape.cncf.io/ and make a mental note of the number of projects in the CNCF landscape.

## 3.3.2  OpenShift Container Platform Compared to Kubernetes ##

<table style="width:100%">
  <tr>
    <th><b>Feature / Aspect</b></th>
    <th><b>Kubernetes</b></th>
    <th><b>Openshift Container Platform</b></th>
  </tr>
  <tr>
    <td>Kubernetes support</td>
    <td>100% compatible</td>
    <td>100% compatible</td>
  </tr>
  <tr>
    <td>Licence</td>
    <td>Apache 2.0</td>
    <td>Commercial</td>
  </tr>
  <tr>
    <td>Linux distribution support</td>
    <td>Most debian based distributions</td>
    <td>Red Hat Enterprise Linux (CentOS for OKD)</td>
  </tr>
  <tr>
    <td>Open source version</td>
    <td>Kubernetes is 100% open source</td>
    <td>Openshift Community Edition (OKD)</td>
  </tr>
  <tr>
    <td>Chart installation method</td>
    <td>Helm</td>
    <td>Helm for version < 4.3, operator for version 4.3 onward</td>
  </tr>
  <tr>
    <td>Command line interface</td>
    <td>kubectl</td>
    <td>kubectl and oc</td>
  </tr>
  <tr>
    <td>Single node version</td>
    <td>minikube, kind, microk8s</td>
    <td>minishift</td>
  </tr>
  <tr>
    <td>Default container engine</td>
    <td>containerd</td>
    <td>cri-o</td>
  </tr>
  <tr>
    <td>Built in software to image capability ?</td>
    <td>No</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>Default Software defined network plugin</td>
    <td>Calico</td>
    <td>OpenShift SDN</td>
  </tr>
</table>

<p style="border-bottom: 1px solid lightgrey;"></p>

## 3.4 Storage ##

### 3.4.1 Kubernetes Storage Concepts ###

There are two storage options available when deploying a SQL Server 2019 big data cluster:

- Ephemeral storage

- Persistent volumes

Ephemeral storage, often also referred to as loopback storage, should never be used for production purposes. With ephemeral storage, the second that a pod is rescheduled to run on a different node, any data associated with that pod will be lost. Ephemeral storage should only ever be used for in environments deployed for the purposes of learning Kubernetes. For production use cases persistent volumes should be used.

Three key entities are associated with persistent volumes:

1.	Volume
Mount point for a Linux or Unix file system inside a pod.

2.	Persistent Volume Claim (PVC)
A request for the storage that will underpin the volume.

3.	Persistent Volume (PV)
A construct that maps directly to the underlying storage platform that persistent volume claims consume storage from.
A persistent volume claim associated with a persistent volume is said to be in a ‘Bound’ state. Persistent volumes created via the local-storage storage class are an exception to this rule, this is because binding only takes place once the pod associated with persistent volume claim / persistent volume is scheduled to run on a node.  

The following deployment illustrates the use a volume and persistent volume claim for a SQL Server instance:

```
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: mssql-deployment
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: mssql
    spec:
      terminationGracePeriodSeconds: 1
      containers:
      - name: mssql
        image: mcr.microsoft.com/mssql/server/server:2017-latest
        ports:
        - containerPort: 1433
        env:
        - name: MSSQL_SA_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mssql
              key: SA_PASSWORD
        volumeMounts:
        - name: mssqldb
          mountPath: /var/opt/mssql
      volumes:
      - name: mssqldb
        persistentVolumeClaim:
          claimName: mssql-data
---
apiVersion: v1
kind: Service
metadata:
  name: mssql-deployment
spec:
  selector:
    app: mssql
  ports:
  - protocol: TCP
    port: 1433
    targetPort: 1433
  type: LoadBalancer
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mssql-data
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 8Gi
  storageClassName: my-block-storage-class
```

### 3.4.2 Manual and Automatic Provisioning ###

Persistent Volumes can be provisioned in one of two different ways:

- **manually**

  This requires that the cluster administrator must undertake manual activities in order to create the persistent volume.
  
- **automatically**

  Under an automatic provisioning scheme, once a persistent volume claim is created, a persistent volume is created automatically and the two are bound.

### 3.4.3 Storage Classes ###

When using persistent volumes, something known as a “Storage class” must be specified and a SQL Server 2019 big data cluster is no exception to this. Simply put, each storage platform that can be used to allocate storage to the cluster has its own storage class. Furthermore, the Kubernetes API allows users to create their own storage classes. There are two fundamental components in a SQL Server 2019 big data cluster that consume storage:

- **The storage pool** 

  For the storage of unstructured data in HDFS parquet format

- **The data pool**

  For the storage of traditional SQL Server data
  
  **Use Case: Collecting and Processing Telemetry Data**
  
  Imagine an application which collects log files associated with telemetry data from Internet of Things (IOT) like devices. The log files the application generates may account for hundreds of terabytes, even petabytes of data. We want to avoid paying the ‘ACID’ tax of storing this data in a relational database, therefore the best place for this data to land is in the storage pool. Once the telemetry data has been collected, we may then wish to aggregate this data for querying via T-SQL. There are two distinct patterns of usage here:

  - We want to use the raw horse power of Spark to perform the bulk of the processing in the storage pool, a storage class associated with a platform optimized for high IO bandwidth is the best   fit for this purpose.

  - We then want to aggregate the data in the data pool for rapid querying, a storage class associated with a storage platform optimized for low latency is ideally suited for this task.

  - Only a small subset of the data is being used for test and development purposes and because our production grade storage comes at a premium, we might want to use a storage class associated with a cheaper storage platform for this purpose.

**Reclaim Policy**

A [reclaim policy](https://kubernetes.io/docs/tasks/administer-cluster/change-pv-reclaim-policy/) is an attribute of a storage class that specifies what happens to persistent volume when there are no persistent volume claims bound to it. For storage classes that use dynamic provisioning the default policy is delete. As a best practices Microsoft recommend that the reclaim policy is set to 'Retain'.

### 3.4.4 Pod Mobility ###

Pods can either be stateless or stateful. One of the most fundamental tasks that Kubernetes carries out is to ensure that the desired state of a pod in terms of replicas and its actual state are one of the same. Pods typically run in either a ReplicaSet or a StatefulSet, if a replica dies by a node going offline for example, Kubernetes will schedule a new pod to run on a healthy node: 

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_3_4_stateless.png?raw=true">

Things become more nuanced once state is involved. When a pod that is stateful is scheduled to run on a different node, the state associated with that pod needs to ‘Follow’ it from its original node to its new node. This can be achieved in one of two ways.
 
- **Storage Replication**

Storage is replicated between nodes, such that if a pod needs to be rescheduled, it can be scheduled to run on a node that its state has been replicated to.

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_3_4_stateful_replicated.PNG?raw=true">

- **Shared Storage**

Each node in the cluster has access to the same storage. When a node fails, a pod can be re-scheduled to any other worker node in the cluster:

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_3_4_stateful_shared.PNG?raw=true">

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Investigate The Storage Objects Associated With Your Workshop Cluster</b></p>

In this activity we will look at the different storage objects associated with your sandbox environment.
 
<p><img style="margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/checkmark.png?raw=true"><b>Steps</b></p>

Use the kubectl cheat sheet to  familiarise yourself with various kubectl commands in order to carry out the following on the jump server:

1. List the storage classes available to the workshop Kubernetes cluster

2. List the persistent volume claims present for the workshop SQL Server 2019 big data cluster

3. From the list of persistent volume claims obtained in the previous step, pick a persistent volume claim and inspect it in detail using kubectl describe.

4. List the persistent volumes present for the workshop SQL Server 2019 big data cluster.
 
### 3.4.6 Access Modes ###

Microsoft database platform professionals will be familiar with the concept of CREATE DATABASE FOR ATTACH:

```
CREATE DATABASE MyAdventureWorks   
 ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),
    (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')
FOR ATTACH;
```

This raises the question; if the persistent volumes for a kubernetes cluster already exist, can this be attached to a big data cluster ?. The answer is that this depends on what is known as the “Access mode” for the persistent volume, of which there are three types:

- **ReadWriteOnce**

  The volume can be mounted as read-write by a single node, this is usually associated with block storage platforms; the type of storage that SQL Server usually runs on that is typically accessed via the iSCSI or the Fiber Channel storage protocols.

- **ReadOnlyMany**

  The volume can be mounted read-only by many nodes. This access mode and ReadWriteMany are usually associated with file-based storage platforms, such platforms are usually accessed via the NFS or SMB protocols.

- **ReadWriteMany**

  The volume can be mounted as read-write by many nodes

### 3.4.7 StatefulSets ###

The architecture of a SQL Server 2019 big data cluster contains components that are clustered by nature, such as storage pods in the storage pool:

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_4_7_bdc_architecture.PNG?raw=true">

Components of an application that are clustered have some special requirements which are not catered for by ReplicaSets. Per the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/), clustered applications usually exhibit one or more of the following requirements:

- Stable, unique network identifiers.

- Stable, persistent storage.

- Ordered, graceful deployment and scaling.

- Ordered, automated rolling updates.

A key feature of a StatefulSet is that each member of a cluster application requires its own persistent volume claim, for this very reason, a StatefulSet uses a persistent volume claim template:

```
volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "my-storage-class"
      resources:
        requests:
          storage: 1Gi
```		  

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Working With Statefulsets</b></p>

1. List the statefulsets present on your sandbox Kubernetes cluster:
```
kubectl get statefulset
```
2. Open the file create-statefulset.yaml, this should be present in the home directory of your sandbox user, use either nano or vi for this purpose. Note the kind of object this is and the volume claim template at the bottom of the file.

3. Create a statefulset using the following command:
```
kubectl apply -f create-statefulset.yaml
```
4. List the persistent volume claims, why are there three of these associated with the statefulset that was just created ?.

### 3.4.8 Considerations for Choosing Storage ### 

- **cost**
  - Is this CAPEX, OPEX, priced on capacity and / or IOPS ?.

- **availability**
  - How available is the platform to serve IO in the event that it suffers a component failure ?.
  - Can the platform still serve IO if a data center or availability zone is lost ?.

- **durability**
  - How durable is the data once it is written ?.

- **performance**
  - Does the storage platform meet the latency / IO bandwidth requirements of the application ?.

- **security**
  - What security features does the storage platform come with ?.
  - If a Kubernetes cluster to be used in a regulated industry that mandates certain security certifications, does the platform adher to these ?.

- **supportability**
  - Is the platform open source or commercially supported ?.
  - Does the organization the kubernetes cluster is deployed at belong to a regulated industry ?

- **managability**
  - How easy is the platform to manage ?.
  - What management tools does the platform come with ?.
  - How easy is it to add storage capacity to the platform ?. 
  - What data protection tools does the platform come with ?.
  - Does the platform require any scripting / programming expertise in order to manage it ?.
  - Does the platform need to provide integration for any existing management frameworks and / or monitoring solutions ?.

- **interoperability**
  - Does the storage platform support any industry standard interfaces ?, Kubernetes is moving towards the container storage interface (CSI) as a standard, 
  - platforms that support this can be seemlessly interchanged.
  - Does the platform need to provide interopability with existing infrastructure, virtualized infrastructure for example.
  - Does the organization have a preference for storage protocol support; iSCSI, Fiber Channel, NFS, SMB etc, if so does the platform support this ?.

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Utilising Kubernetes Persistent Storage Volumes</b></p>

1. Following the plugin instructions in section 2 in order to install the Kubernetes storage plugin.

2. A test-pvc.yaml file should be present in the home directory of the sandpit environmen. The contents of the file should be as follows:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: test-pvc
spec:
  accessModes:
   - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
  storageClassName: block-storage-class
```

The storage class name will vary depending on which vendor has supplied the workshop hardware.

3. Create the persistent volume claim as follows:
```
kubectl apply -f test-pvc.yaml
```

4. List all the persistent volume claims present in your sandpit environment cluster:
```
kubectl get pvc --all-namespaces
```

Note the status of test-pvc persistent volume claim.

5. Obtain a detailed description of the test-pvc persistent volume claim:
```
kubectl desc pvc test-pvc
```

6. List all the persistent volumes present in your sandpit environment cluster:
```
kubectl get pv --all-namespaces
```

For a storage class that provides automatic provisioning, the persistent volume is automatically created for the test-pvc volume.

<p style="border-bottom: 1px solid lightgrey;"></p>

## 3.6 Management Of Sensitive Information ##

Key to managing sensitive information such as passwords is the Kubernetes object type of Secret. Secrets encrypt information which is stored in etcd, at the time when a secret is required it is injected into a pod(s) are made available via a temporary file system.

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Working With Secrets</b></p>

In this activity we will look at what Secret objects come with a big data cluster and create a secret.

<p><img style="margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/checkmark.png?raw=true"><b>Steps</b></p>

1. Connect to your workshop Ubuntu virtual machine using a ssh client.

2. List the secrets associated with your sandbox environment big data cluster:
```
kubectl get secret -n mssql-cluster
```
3. Now create a secret:
```
kubectl create secret generic mssql --from-literal=SA_PASSWORD="MySuperSecretP@ssw0rd"
```
## 3.7 Services ##

A service is an abstraction which defines a logical set of Pods and a policy by which to access them, or more simply put, a service provides the means by which clients running **outside** of a Kubernetes cluster to consume functionality provided by pods running **inside** the cluster.

There are three types of service:

- **ClusterIP**: this provides a virtual ip address that is only accessible from within the cluster. The motivation for this type of service is to provide pods that form different parts of an application, for example the front end back ends of the application, the means of communicating via a stable ip address. This is the default service.

- **NodePort**: exposes the service via a static port on each node.

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_7_1_node_port.PNG?raw=true">

- **LoadBalancer**: exposes the service via a single load balancer endpoint, this in turn routes traffics to pods running inside the cluster.

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_7_2_load_balancer.PNG?raw=true">

- **ExternalName**: Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up.

When creating a Kubernetes cluster using Kubernetes-As-A-Service such as Azure Kubernetes Service, the default type of service that expose a cluster's pods to the outside world is LoadBalancer.
By default the service type for Kubernetes clusters deployed on-premises, is NodePort. The term for the component that manages external access to a cluster in the context of routing, is ["Ingress controller"](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/).  

<p><img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/point1.png?raw=true"><b>Activity: Working With Services</b></p>

TODO: enter brief description of activity.

<p><img style="margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/graphics/checkmark.png?raw=true"><b>Steps</b></p>

## 3.8 Disaster Recovery ##

The ecosystem in which a SQL Server 2019 big data cluster runs on Kubernetes comprises of different layers:

<img style="float: left; margin: 0px 15px 15px 0px;" src="https://github.com/microsoft/sqlworkshops/blob/master/k8stobdc/graphics/3_7_1_tech_stack.PNG?raw=true">

In the context of Kubernetes, state is stored in several places:

1. Persistent volumes for application data.

2. etcd for the entire configuration of the cluster, including secrets and configuration maps.

3. Certificates; the communication between many of the key components in a cluster involves SSL certificates, such as when kubelets talk to a master node.

Options for backing up etcd include:

- **Backup the directory where your cluster's etcd data resides**, this could involve the use of storage snapshot technology

- **etcdctl**, this allows snapshots of etcd to be taken, restoring a etcd cluster involves a new instance of the cluster being created which incurrs downtime.

- **[VMware Velero](https://github.com/vmware-tanzu/velero)** (formally Heptio Ark), this integrates with 3rd party storage APIs in order to backup the entire state of a Kubernetes cluster.

## 3.8 Kubernetes Best Practices ##

Now that many of the most important Kubernetes concepts have been covered, what exactly does a Kubernetes cluster that is fit for production puproses look like ?, the simple answer is that a production grade cluster should adhere to many of the following points:

- There should be atleast two master nodes.

- Each master node should have a NoSchedule taint.

- There should be atleast 3 etcd instances.

- The cluster should have a storage plugin installed with an associated storage class that has a retain policy on Retain.

- Always use the latest GA verison of Kubernetes.

- Do not deploy the Kubernetes dashboard without using RBAC.

- Use kubectl proxy as the peferred method of exposing the Kubernetes dashboard, otherwise look at using an authenticating proxy or a NodePort service for this purpose.

- Follow [documented](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/) Kubernetes best security practices, this includes checking that role base access is enabled for the cluster, this can be verified with this command:
```
kubectl api-versions | grep rbac
```
- Make provision for extra node capacity to allow for pod rescheduling in the event of a node failure **and** test this prior to putting a cluster into production.

- General disaster recovery best practices still apply as per any platform, **always test your backups**.

## 3.9 Troubleshooting ##
