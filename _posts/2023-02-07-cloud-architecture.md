---
layout: post
title: Cloud computing architecture
---

![image](https://user-images.githubusercontent.com/109908559/217190814-888b46ac-383f-4030-977e-e0dca9cc8ec1.png)

### IT Resources

- physical server
- virtuel server
- software program
- service
- storage device
- network device

### Cloud consumer

![image](https://user-images.githubusercontent.com/109908559/217191286-f7f5f9d4-ad4e-4093-999b-5eab89dd8677.png)

### Access to resources

A cloud service with a published technical interface is being accessed by a consumer outside of the cloud (left). A cloud
service that exists as a virtual server is also being accessed from outside of the cloud’s boundary (right). The cloud service
on the left is likely being invoked by a consumer program that was designed to access the cloud service’s published technical
interface. The cloud service on the right may be accessed by a human user that has remotely logged on to the virtual server.

![image](https://user-images.githubusercontent.com/109908559/217192023-11fee077-e76f-492d-a23d-239e1633c5f1.png)

### Scaling

#### Scale up or vertical scaling

You also can scale up when you add *more memory*, *more network throughput*, and
*other resources to a single node*. Scaling up indefinitely eventually leads you to an architecture with a single powerful supercomputer.

For instance, you might replace a node in a cloud-based system that has a dual-processor machine instance equivalence
with a quad-processor machine instance equivalence. 

#### Scale out or horizontal scaling

*Adding capacity to a system by adding more individual nodes*.

Scaling out indefinitely leads you to an architecture with a large number of servers (a server farm), which is the model that many
cloud and grid computer networks use.

For instance, in a system where you have a dual-processor machine instance, you would scale out by adding more dual-processor machines instances or some other type of commodity system.

### Load balancing

Load balancing is the process of distributing workloads across multiple computing resources, such as servers, to optimize resource utilization, maximize throughput, minimize response time, and avoid overload. Load balancing can be achieved through various methods, including round-robin, least connections, IP hash, and geographic hash. The goal of load balancing is to ensure that no single resource is overwhelmed, leading to improved reliability and availability of the overall system.

### Workload distribution: monitoring, hypervising, resoure pooling

A redundant copy of Cloud Service $A$ is implemented on Virtual Server $B$. The *load balancer* intercepts cloud service
consumer requests and directs them to both Virtual Servers $A$ and $B$ to ensure even *workload distribution*.

*A workload simulates the ability of a certain type of real or physical server to do an amount of work.*
- Transactions Per Minute (TPM)
- Disk I/Os measured
- RAM consumed under load in MB
- network throughput and latency...

• *Audit Monitor* - When distributing runtime workloads, the type and geographical
location of the IT resources that process the data can determine whether
monitoring is necessary to fulfill legal and regulatory requirements.
• *Cloud Usage Monitor* - Various monitors can be involved to carry out runtime
workload tracking and data processing.
• *Hypervisor* - Workloads between hypervisors and the virtual servers that they
host may require distribution. => virtualization & containers
• *Logical Network Perimeter* - The logical network perimeter isolates cloud
consumer network boundaries in relation to how and where workloads are
distributed.
• *Resource Cluster* - Clustered IT resources in active mode are commonly used to
support workload balancing between different cluster nodes.
• *Resource Replication* - This mechanism can generate new in-stances of
virtualized IT resources in response to runtime workload distribution demands.

### Resource Pooling

Identical IT resources are grouped and maintained by a system that automatically ensures that they remain synchronized

![image](https://user-images.githubusercontent.com/109908559/217198051-b92cc8a5-d260-42fb-b979-3abcadf84aed.png)

### Dynamic scalability

The dynamic scalability architecture is an architectural model based on a system of predefined scaling
conditions that trigger the *dynamic allocation* of IT resources from *resource pools*. Dynamic allocation enables variable utilization as dictated by usage demand *fluctuations*, since unnecessary IT resources are efficiently
reclaimed without requiring manual interaction.

![image](https://user-images.githubusercontent.com/109908559/217199887-f8096f1c-d036-4671-94f6-19dba668b8a8.png)

The number of requests coming from cloud service consumers increases (3). The workload exceeds the performance thresholds. The automated *scaling listener*
determines the next course of action based on a predefined *scaling policy* (4). If the cloud service implementation is deemed eligible for additional scaling, the
automated scaling listener initiates the *scaling process* (5).

![image](https://user-images.githubusercontent.com/109908559/217200118-41c2569b-b031-4387-9731-8a064f0e6f3d.png)

The automated scaling listener sends a signal to the *resource replication* mechanism (6), which creates more instances of the cloud service (7). Now that the increased workload has been accommodated, the automated scaling listener resumes monitoring and detracting and adding IT resources, as required (8)

### Elastic resource capacity

The elastic resource capacity architecture is primarily related to the
*dynamic provisioning of virtual servers*, using a system that allocates
and reclaims CPUs and RAM in immediate response to the fluctuating
processing requirements of hosted IT re-sources
