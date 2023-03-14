In this demo, we will create a simple application that requires persistent storage and use K8s to deploy and manage the application. 
We will use a PVC to dynamically provision storage for the application and a PV to represent the physical storage resource.

##### Create a Persistent Volume (PV) YAML manifest file:

<pre class="code-block">
yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-demo
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /data/pv-demo
</pre>

This manifest creates a PV named pv-demo with a storage capacity of 1Gi, access mode of ReadWriteOnce, 
and using a hostPath volume type to represent the physical storage resource.

#### Create a Persistent Volume Claim (PVC) YAML manifest file:

<pre class="code-block">
yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-demo
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
</pre>    
      
This manifest creates a PVC named pvc-demo with a request for 1Gi of storage and a ReadWriteOnce access mode.

##### Create a Deployment YAML manifest file:

<pre class="code-block">
yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app-demo
  template:
    metadata:
      labels:
        app: app-demo
    spec:
      containers:
        - name: app
          image: nginx
          ports:
            - containerPort: 80
          volumeMounts:
            - name: app-data
              mountPath: /usr/share/nginx/html
      volumes:
        - name: app-data
          persistentVolumeClaim:
            claimName: pvc-demo     
</pre> 

This manifest creates a Deployment named app-demo with one replica and a container named app running the nginx image. 
The manifest also specifies a volume mount named app-data at the /usr/share/nginx/html mount path and a volume named app-data that uses the PVC named pvc-demo.

##### Apply the manifests using the kubectl apply command:

<pre class="code-block">
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
kubectl apply -f deployment.yaml
</pre>

These commands apply the PV, PVC, and Deployment YAML manifest files to the K8s cluster.

##### Verify the application is running and using persistent storage:

<pre class="code-block">
sql
kubectl get deployments
kubectl get pods
kubectl exec -it <pod-name> -- sh
df -h
</pre>

These commands list the Deployments and Pods in the K8s cluster and allow us to access the shell of the running container.
The df -h command is used to display the file system disk space usage and should show the persistent volume mounted at /usr/share/nginx/html.

### Conclusion
In this demo, we have created a simple application that requires persistent storage and used K8s to deploy and manage the application. 
We have used a PVC to dynamically provision storage for the application and a PV to represent the physical storage resource. 
We have also demonstrated how to use ConfigMap and Secret as volume types and how to define different classes of storage using a Storage Class (SC).
With these tools, developers can easily manage and scale their applications that require persistent storage in K8s.
