### Deploying Stateful Apps with StatefulSet
<img src=https://user-images.githubusercontent.com/89149327/225125848-03995549-8a94-4c0b-a4ae-72183d9c8dd7.png alt="example image" width="500" height="300">

#### What is StatefulSet?
A StatefulSet is a Kubernetes object used for deploying and scaling stateful applications. 
It provides guarantees about the identity of the Pods it manages, and it ensures that the Pods are deployed in a specific order.
StatefulSets are useful for deploying applications that require stable network identities, persistent storage, and ordered deployment.

#### Difference of stateless and stateful applications
Stateless applications do not require the state to be saved in between requests, and they can run on any node in the cluster. 
In contrast, stateful applications require the state to be saved between requests, and they must be deployed on specific nodes in the cluster.

#### Deployment of stateful and stateless apps
Deployment is a Kubernetes object used for deploying and scaling stateless applications. It creates multiple identical Pods and provides load balancing across them. Deployment is useful for applications that can run on any node in the cluster and do not require stateful data to be saved between requests.

#### Deployment vs StatefulSet
Deployment is used for deploying and scaling stateless applications, while StatefulSet is used for deploying and scaling stateful applications. 
StatefulSet provides guarantees about the identity of the Pods it manages, ensures that the Pods are deployed in a specific order, 
and provides stable network identities and persistent storage.

![image](https://user-images.githubusercontent.com/89149327/225126143-90527778-a68d-48dd-a1b3-51609fa602ab.png)

#### Pod Identity
Pod Identity is the unique identifier assigned to a Pod by Kubernetes. 
It is based on the name of the Pod and the StatefulSet that created it.
Pod Identity is useful for stateful applications because it ensures that each Pod has a unique identity and can be accessed consistently.

#### Scaling database applications: Master and Worker Pods
Scaling database applications requires a different approach than scaling stateless applications. 
In a database application, the data must be saved between requests, and the database must be distributed across multiple nodes for performance and scalability. 
Master and Worker Pods are used for scaling database applications. The Master Pod is responsible for managing the database, 
while the Worker Pods are responsible for reading and writing data.

#### Pod state, Pod Identifier
Pod state is the current status of a Pod, such as running, terminated, or failed. 
Pod Identifier is the unique identifier assigned to a Pod by Kubernetes based on the name of the Pod and the StatefulSet that created it.

##### 2 Pod endpoints
Pod endpoints are used for connecting to Pods in a StatefulSet. 
There are two types of endpoints: 
- Headless and Stateful. 

Headless endpoints return the IP addresses of each Pod in the StatefulSet, while Stateful endpoints return the DNS names of each Pod in the StatefulSet. 
Headless endpoints are useful for applications that require direct access to each Pod, 
while Stateful endpoints are useful for applications that require load balancing across the Pods.
