<details>
 <summary><h3> 🔥 Organizing your components with K8s Namespaces 🔥 </h3></summary>


Kubernetes is an open-source container orchestration platform that provides various features to manage containerized applications.
One of the essential features of Kubernetes is namespaces, which allow users to organize their resources and components within a cluster.

#### What is a Namespace?
A Namespace is a virtual cluster within a Kubernetes cluster that provides a way to divide cluster resources between multiple users or teams. 
It creates a scope for names and helps in organizing resources based on their functionalities. 
In other words, Namespaces provide a way to isolate objects within a Kubernetes cluster.

#### 4 Default Namespaces
Kubernetes provides four default Namespaces, which are:

1. Default: It is the default Namespace where all the objects are created if no other Namespace is specified.
2. kube-system: It contains objects created by the Kubernetes system, such as DaemonSets, ConfigMaps, and Nodes.
3. kube-public: It contains public information accessible to all users.
4. kube-node-lease: It contains node lease information that is used by the Kubernetes controller manager.
#### Create a Namespace
A Namespace can be created using the kubectl command-line tool. The following command creates a Namespace named my-namespace.

cpp
Copy code
kubectl create namespace my-namespace
 #### Why to use Namespaces? 4 Use Cases

1. Resource Isolation: Namespaces provide resource isolation by creating virtual clusters within a Kubernetes cluster, 
making it easier to manage and organize resources for multiple users or teams.
2. Access Control: Namespaces allow users to set access controls for their resources, providing enhanced security within the cluster.
3. Multi-Tenancy: Namespaces enable multiple teams or tenants to share the same cluster infrastructure while maintaining isolation.
4. Resource Quotas: Namespaces enable the allocation of resource quotas to different teams, preventing one team from consuming all available resources.
#### Characteristics of Namespaces

- Namespaces have unique names that can be up to 63 characters long.
- Namespaces can contain objects such as Pods, Services, ConfigMaps, and more.
- Objects within a Namespace can reference other objects within the same Namespace or different Namespaces.
- Namespaces provide resource isolation, access control, multi-tenancy, and resource quotas.
#### Create Components in Namespaces
When creating a component, you can specify the Namespace by using the --namespace option with kubectl. 
For example, the following command creates a Pod named my-pod in the my-namespace Namespace.

perl
Copy code
kubectl run my-pod --image=my-image --namespace=my-namespace
#### Change Active Namespace
The current active Namespace can be changed using the kubectl config command. 
For example, the following command sets the active Namespace to my-namespace.

cpp
Copy code
kubectl config set-context --current --namespace=my-namespace
In conclusion, Namespaces are a powerful feature of Kubernetes that enable users to organize resources, provide resource isolation, access control, multi-tenancy, 
and resource quotas. They are an essential tool for managing complex containerized applications in Kubernetes
