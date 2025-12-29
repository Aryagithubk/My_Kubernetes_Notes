Containers vs. Virtual Machines
Understanding the differences between Docker containers and virtual machines (VMs) is crucial. Here's a brief comparison:

In a Docker-based architecture, the flow is:
Hardware → Operating System → Docker → Containers (with their own libraries and dependencies)
In a VM setup, the flow is:
Hardware → Host Operating System → Hypervisor (e.g., ESXi) → Virtual Machines (each with its own guest OS, libraries, and applications)

Docker containers are lightweight (typically measured in megabytes) and boot in seconds. In contrast, VMs require more disk space (often in gigabytes) and take minutes to boot since each VM runs a complete operating system. While Docker containers provide less isolation—by sharing the host kernel—VMs offer complete isolation with separate OS instances.

An image is a template, similar to a VM template, used to create one or more containers. Containers are the running instances of these images, each operating as an isolated environment with its own processes.

Container orchestration platforms provide the necessary resources and capabilities by managing container connectivity and autoscaling seamlessly.Container orchestration automates the deployment, scaling, and management of containerized applications.

Kubernetes stands out as the industry favorite. Although its initial setup might be more involved, Kubernetes offers extensive customization for deployments and can manage intricate architectures with ease. It is supported by all major public cloud providers—Google Cloud Platform, Azure, and AWS.

Kubernetes Architecture

A node is a physical or virtual machine where Kubernetes is installed. Acting as a worker in your cluster, nodes run your containerized applications.To ensure high availability, it is important to have multiple nodes grouped into a cluster. In a clustered environment, if one node fails, the application can continue running on other nodes while the workload is distributed evenly.

Managing a cluster requires a central control point, which is where the master node comes into play. The master node hosts components that control and monitor the cluster’s state.

several components of kubernetes:

API Server: The front end for Kubernetes.

etcd Key-Value Store: A distributed, reliable store for all cluster data.etcd ensures that cluster configuration is synchronized across all the nodes. It also implements locking mechanisms to avoid conflicts between multiple masters.

kubelet: An agent that runs on each node, ensuring containers are running as expected.

Container Runtime: Software such as Docker that runs the containers.

Controllers basically "Watchers" hote hain jo cluster ki current state ko monitor karte hain aur check karte hain ki sab kuch user (admin) ke desired state (jo hum chahte hain) jaisa hai ya nahi, agar difference ho to woh automatic changes karte hain, taaki system hamesha sahi condition mein rahe.

Scheduler:The scheduler is responsible for detecting newly created container requests and assigning them to the most suitable nodes based on available resources and defined policies.

The master node runs critical components such as the kube-apiserver, control manager, scheduler, and the etcd key-value store. In contrast, worker nodes host the kubelet agent and the container runtime.

History of Containers

Docker (container runtime) was the leading container tool.Kubernetes was initially designed to orchestrate Docker containers, creating a tight coupling between the two. Kubernetes introduced the Container Runtime Interface (CRI), to integrate any container runtime easily. It has two key standards:

image spec = Outlines how container images should be built.
Runtime Spec: Establishes the guidelines for developing a container runtime.

Docker has runtime component called runc which is responsible for all internal activities of docker and is managed by daemon called containerd. As Instead of users or higher-level systems interacting directly with the complex, low-level runc, they interact with Containerd. Containerd handles critical tasks such as:

Image Management: Pushing and pulling container images from registries (e.g., Docker Hub).
Container Lifecycle Management: Creating, starting, stopping, pausing, and deleting containers.
Integration: Providing an API for higher-level orchestrators, most famously Kubernetes, to manage containers effectively. 

Containerd originated as a component of Docker but has evolved into an independent project under the Cloud Native Computing Foundation with graduated status. It can be installed as a standalone runtime, making it a preferred alternative for users who do not need Docker’s complete set of features.

When using Containerd, you have access to the CTR tool—a CLI primarily focused on debugging rather than everyday container management.

To enhance the user experience, the nerdctl CLI provides Docker-like commands.

crictl: A Kubernetes-maintained debugging and inspection tool for any CRI-compatible runtime.

Installation 

Minikube is the easiest way to launch a local Kubernetes cluster.Minikube packages the complete Kubernetes bundle into an ISO image that is automatically downloaded and deployed using its command-line utility. It integrates seamlessly with various virtualization platforms.To interact with your Kubernetes cluster, you also need to install the kubectl command-line tool.Hypervisor should be installed first before minikube.


Hypervisor - A virtualization tool such as VirtualBox, Hyper-V, or KVM.
kubectl - The official Kubernetes command-line tool.
Minikube executable - The utility that automates ISO download and cluster deployment.

Kubernetes resource definition files follow a consistent structure and always include four top-level fields:

apiVersion - shows kubernetes API version.
kind - type of kubernetes object to be created.
metadata - you provide key information about the Kubernetes object.
spec - describes the desired state of the object.

