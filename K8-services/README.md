<details>
 <summary><h3> Demo </h3></summary>


In this demo, we will create a Kubernetes cluster with two Pods and a Service to expose them to the network.

Prerequisites
- A Kubernetes cluster
- kubectl CLI tool installed and configured
-  Basic knowledge of Kubernetes concepts
### Step 1: Create two Pods
We will create two Pods with a simple Nginx web server running inside them. For simplicity, we will use the Nginx image from Docker Hub.

Create a file named pod.yaml and add the following content to it:
  
<pre class="code-block">
yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod1
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
</pre>

Save the file and create the Pod by running the following command:

<pre class="code-block">
kubectl apply -f pod.yaml
</pre>

Repeat the above steps to create a second Pod with a different name, such as nginx-pod2.

Step 2: Create a Service
We will now create a Service to expose the two Pods to the network. The Service will act as a load balancer and route traffic to the Pods.

Create a file named service.yaml and add the following content to it:

<pre class="code-block">
yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
  - name: http
    port: 80
    targetPort: 80
</pre>

Save the file and create the Service by running the following command:
  
<pre class="code-block">
kubectl apply -f service.yaml
</pre>

### Step 3: Test the Service
We can now test the Service by accessing it from within the cluster. To do this, we will create a temporary Pod and use it to make a request to the Service.

Create a file named test.yaml and add the following content to it:
  
<pre class="code-block">
yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pod
spec:
  containers:
  - name: busybox
    image: busybox
    command: ['sh', '-c', 'wget -qO- nginx-service']
</pre>

Save the file and create the temporary Pod by running the following command:
  
<pre class="code-block">
kubectl apply -f test.yaml
</pre>

Check the logs of the Pod to see the response from the Service:

<pre class="code-block">
kubectl logs test-pod
</pre>

You should see the HTML content of the Nginx web server running inside one of the two Pods.

### Step 4: Expose the Service to the Internet
To expose the Service to the Internet, we can use one of the following Service types: NodePort, LoadBalancer, or ExternalName.

For this demo, we will use the NodePort type, which will allocate a port on each worker node and route traffic to the Service.

Update the service.yaml file to use the NodePort type:

<pre class="code-block">
yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
  - name: http
    port: 80
    targetPort: 80
</pre>
Save the file and apply the changes by running the following command:

<pre class="code-block">
kubectl apply -f service.yaml
</pre>

Get the NodePort allocated to the Service by running the following command:

<pre class="code-block">
csharp
kubectl get service nginx-service
</pre>

You should see an output similar to the following:
<pre class="code-block">
scss
NAME            TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
nginx-service   NodePort   10
</pre>
