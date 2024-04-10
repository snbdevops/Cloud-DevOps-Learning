# 1 Kubernetes for Beginers by Mumshad Sir

Kubernetes = Containers + Orchesteration

### I) Contaiers: Completely Isolated Environement. As in they can have their own processes or services, their own networking interfaces, their own mounts, just like virtual machines, except they're all shared the same operating system kernel.

If you look at operating systems like ubuntu, fedora, Suse, or CentOS, they all consist of two things an OS kernel and a set of software. The operating system kernel is responsible for interacting with the underlying hardware, while the OS kernel remains the same, which is Linux. In this case, it's the software above it that makes these operating systems different. 

The software may consist of a different user interface drivers, compilers, file managers, developer tools, etc. so you have a common Linux kernel shared across all operating systems, and some custom software that differentiates operating systems from each other.

The main purpose of Docker is to containerize applications and to ship them and run them.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/0019a3f3-b1e2-4663-9873-949d1a746e49)


### II) Orchesteration:

How do you run it in production?
What if your application relies on other containers such as databases or messaging services or other backend services?
What if the number of users increase and you need to scale your application? How do you scale down when the load decreases? 


To enable these functionalities, You need an underlying platform with a set of resources and capabilities. The platform needs to orchestrate the connectivity between the containers and automatically scale up or down based on the load.

This whole process of automatically deploying and managing containers is known as Container Orchestration.

Below are the few Container Orchestration tools - 
#Docker Swarm by Docker
#Kubernetes by google
#MESOS by apache

**There are various advantages of Container Orchestration.**
  -Your application is now highly available as hardware failures to not bring your application down because we have multiple instances of your application running on different nodes.
  -The user traffic is load balanced across the various containers.
  -When demand increases, deploy more instances of the applications seamlessly and within a matter of seconds.

We can achieve all this by Kubernetes.

Kubernetes is a container orchestration technology used to **orchestrate the deployment** and **management of hundreds and thousands of containers in a clustered environment**.

We have the ability to perform all the above advantages at a service level when we run out of hardware resources, scale the number of underlying nodes up or down without having to take down the application and do all of these easily with a set of declarative object configuration files. Thats it.

**Kubernetes Architecture**

1) Nodes

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/d281ffc1-59d8-4be1-a083-55d7c836b13b)

2) Cluster

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/cc7c7e95-ad85-48f3-bf0f-63d20a10c907)

3) Master

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/1b63d299-6216-4270-ac17-06b7c249874a)

4) Kubernetes Components

a) API Server: Acts as front-end for kubernetes.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/ef0f1028-a5a9-4393-bf7d-1ad0131ecc42)

b) etcd: Key-value store used by kubernetes to store data used to manage the cluster.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/c5892793-3b83-4a0d-b151-23e76c5cafbd)

c) schedulers: Distributing works to multiple nodes. It looks for newly created continers and assign them to nodes.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/07f195ae-ea29-4b76-8da0-95d26fbf65af)

d) Controllers: Controllers are brain behind orchestration. They are responsible for noticing and responding when nodes, containers or end points goes down.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/51a0f141-b4cd-44e1-8a95-ab2e5ff7dd06)

e) Container Runtimes: Underline software that is used to run containers. In our case here, its docker.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/d2dcf007-6d1b-4524-abdc-1a526e1fcd2c)

f) Kubelet: Its the agent that runs on each node in the cluster. The agents makes sure that the containers are running in the nodes as expected.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/3d76fd1a-4197-40cc-a733-6649c7d4ccf5)

5) Master vs Worker Nodes

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/2e983cef-4e99-4fa3-bf80-c3b5be32bb97)

6) Kubectl

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/c585519d-2d1b-4b6d-8876-1c9b261c03bb)

**==> PODS**

As we are aware with Kubernetes, our ultimate aim is to deploy our application in the form of containers on a set of machines that are configured as worker nodes in a cluster.

However, Kubernetes does not deploy containers directly on the worker nodes. The containers are **encapsulated** into a Kubernetes object known as pods. A pod is a single instance of an application. A pod is the smallest object that you can create in Kubernetes.

Pods usually have a 1 to 1 relationship with containers running your application to scale up, you create new pods and to scale down you delete existing pods.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/f81dfa48-5135-450c-9922-0875d99ae433)

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/09bb3042-eee2-424c-9881-ffd43adb0825)

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/b75c2e60-e3eb-4cde-93f4-edad3baefd62)

**Multi-Container Pod**
If our intention was to scale our application, then we would need to create additional pods.

But sometimes we might have a scenario where we have a helper container that might be doing some kind of supporting task for our web application, such as processing a user entered data processing a file uploaded by the user, etc.

And we want these helper containers to live alongside our application container?

In that case, we can have both of these containers part of the same pod so that when a new application container is created, the helper is also created and when it dies, the helper also dies since they are part of the same pod.

The two containers can also communicate with each other directly by referring to each other as local host since they share the same network space plus, they can easily share the same storage space as well.

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/53a94cb3-e738-4d75-a105-b5ef958d626b)

**Understanding YAML** 
![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/a9491861-528b-4f23-9c5e-b29c9349008e)

**Creating Pod using YAML Based configuration file**

Kubernetes uses YAML files as inputs for the creation of object such as PODs, Replicas, Deployments, services, etc...

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/9f3d037e-2e15-4c85-bfd0-785e860cf51c)

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/15ce0c4f-996d-4ad7-8111-6256e609ae6f)

**` kubectl apply -f pod.yaml `**

**Some Kubernetes Commands**

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/1a6177ae-108e-4db5-90d3-cbb80dc52e70)

**==> Replica Sets**

Replicaset is a object of kubernetes used for HA, Loadbalancing between pods.

Below is the example for replicasets.yaml file -

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/476406c5-ba93-4e9c-9a42-5dd7a6f5365a)

Note: 
1. apiVersion should be 'apps/v1' and NOT just 'v1'.
2. kind should be 'ReplicaSet'. Keep in mind that its case sensetive.
3. Inside spec, there should be 3 parameters - 'replicas','template','selector'. 
4. **replicas** contains number of replicas required. **template** section contains pods details with image details that needs to be created with this replicaset. **selector** contains linking of specific pods with replica sets with the help of 'matchLabels' parameter

**==> Deployments**

![image](https://github.com/snbdevops/Cloud-DevOps-Learning/assets/83505877/17eb4dd3-6bb6-4dfc-a02c-709fc61b7dd0)

Deployment manifest files are similar to replicasets. Just we need to replace kind part from 'ReplicaSet' to 'Deployment'.

# 2 CKA exam preparation by Mumshad Sir
