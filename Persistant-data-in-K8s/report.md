<details>
 <summary><h3> Report </h3></summary>

Kubernetes (K8s) is a popular container orchestration platform used to manage and deploy containerized applications. 
One of the main advantages of using K8s is its ability to handle and scale applications seamlessly. 
However, a challenge that comes with deploying applications in K8s is the need for persistent storage. 
In this report, we will explore the need for persistent storage, the different types of persistent volumes, 
who creates them and when, persistent volume claims, levels of volume abstractions, ConfigMap and Secret as volume types, and storage classes.

#### The Need for Persistent Storage & Storage Requirements
When running applications in K8s, you need persistent storage to ensure data is not lost when a container is terminated.
Persistent storage is also required for stateful applications like databases, where data needs to be stored across container restarts. The storage requirements for K8s applications include:

1. Data Persistence: Data must be preserved even if a container is deleted or recreated.

2. Scalability: Storage must be scalable to accommodate data growth.

3. Accessibility: Data should be easily accessible by all containers in a pod.

4. Reliability: Storage must be reliable and fault-tolerant.

5. Performance: Storage should provide good performance to ensure applications can operate efficiently.

#### Persistent Volume (PV)
In K8s, a Persistent Volume (PV) is a resource that represents a piece of storage in the cluster that has been provisioned by an administrator. 
PVs can be created and managed independently of pods, and their lifecycle is separate from that of the pods that use them.
PVs are defined in a YAML manifest and specify the storage capacity, access modes, and the type of storage.

#### Local vs Remote Volume Types
There are two types of persistent volumes in K8s - local and remote. Local volumes are physically attached to the node that the pod is running on,
while remote volumes are accessed over the network. Local volumes are ideal for applications that require high performance, 
while remote volumes are suitable for applications that require shared access to data.

#### Who Creates the PV and When?
Persistent Volumes are created and managed by administrators, not developers. 
The administrator provisions the storage, creates the PV, and exposes it to developers. 
Once a PV is created, it can be dynamically provisioned by developers using a Persistent Volume Claim (PVC).

#### Persistent Volume Claim (PVC)
A Persistent Volume Claim (PVC) is a request for storage by a developer. PVCs are used to dynamically provision storage for pods. 
A PVC specifies the amount of storage required, access modes, and the storage class to use. 
When a PVC is created, the K8s control plane matches it with a suitable PV and binds the two together.
Once a PVC is bound to a PV, the pod can use the storage specified in the PVC.

#### Levels of Volume Abstractions
There are three levels of volume abstractions in K8s: PV, PVC, and pod volumes. 
PV is the lowest level of abstraction and represents the physical storage resource. PVC is a higher level of abstraction and represents a request for storage.
Pod volumes are the highest level of abstraction and represent the storage that is available to a pod.

#### ConfigMap and Secret as Volume Types
ConfigMap and Secret are two additional volume types in K8s that are used to store configuration data and sensitive data like passwords and API keys. 
ConfigMaps are used to store configuration data in key-value pairs, while secrets are used to store sensitive data like passwords and API keys.

##### Storage Class (SC)
A Storage Class (SC) is a way to define different classes of storage in K8s. 
Each SC is associated with a set of parameters that define the type of storage to use, its performance characteristics, and any other features that are available.
