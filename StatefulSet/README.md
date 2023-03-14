<details>
 <summary><h3> Demo </h3></summary>

In this demo, we will explore deploying stateful applications using StatefulSets in Kubernetes. 
We will create a simple web application with a backend database and deploy it using StatefulSets to ensure that the database maintains its state.

###### Create a StatefulSet YAML manifest file:

<pre class="code-block">
yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: webapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp
  serviceName: "webapp"
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
      - name: web
        image: nginx
        ports:
        - containerPort: 80
        volumeMounts:
        - name: data
          mountPath: /var/www/html
      volumes:
      - name: data
        persistentVolumeClaim:
          claimName: webapp-data
  volumeClaimTemplates:
  - metadata:
      name: webapp-data
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
</pre>

This manifest creates a StatefulSet named webapp with three replicas and a nginx container running as the web server.
The manifest also specifies a persistent volume named webapp-data that is mounted to the container's /var/www/html directory to store the web application's data.

##### Apply the manifest using the kubectl apply command:

<pre class="code-block">
kubectl apply -f statefulset.yaml
</pre>
This command applies the StatefulSet YAML manifest file to the Kubernetes cluster.

##### Verify the StatefulSet is running and the persistent volume is mounted:

<pre class="code-block">
sql
kubectl get statefulsets
kubectl get pods
kubectl exec -it webapp-0 -- sh
ls /var/www/html
</pre>

These commands list the StatefulSet and Pods in the Kubernetes cluster and allow us to access the shell of the running container. 
The ls /var/www/html command verifies that the persistent volume is mounted to the container's /var/www/html directory.

Scale the StatefulSet:

<pre class="code-block">
css
kubectl scale statefulset webapp --replicas=5
</pre>

This command scales the StatefulSet to five replicas.

#### Conclusion
In this demo, we have explored deploying stateful applications using StatefulSets in Kubernetes. 
We have created a simple web application with a backend database and deployed it using StatefulSets to ensure that the database maintains its state.
We have also demonstrated how to scale the StatefulSet and how to verify that the persistent volume is mounted to the container's directory. 
With these tools, developers can easily manage and scale their stateful applications in Kubernetes.
