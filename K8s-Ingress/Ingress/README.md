In Kubernetes, Ingress is a powerful tool that acts as a traffic router to the internal services from external networks. 
It provides a single point of entry for HTTP and HTTPS traffic and routes it to the appropriate internal service based on the request's host and URL path.

##### External Service vs. Ingress:

An external service can be used to expose a Kubernetes service to the internet. 
However, it provides limited features such as only supporting TCP and UDP protocols. 
In contrast, Ingress supports HTTP and HTTPS protocols and provides advanced features like load balancing, SSL termination, and routing rules.

#### Example YAML Config Files for External Service and Ingress:

Below is an example YAML config file for External Service:
<pre class="code-block">
yaml
apiVersion: v1
kind: Service
metadata:
  name: external-service
spec:
  selector:
    app: internal-service
  ports:
    - name: http
      port: 80
      targetPort: 8080
      protocol: TCP
  type: LoadBalancer
</pre>
Below is an example YAML config file for Ingress:
<pre class="code-block">
yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /internal-service
        pathType: Prefix
        backend:
          service:
            name: internal-service
            port:
              name: http
 </pre>
- Internal Service Configuration for Ingress:

The internal service should be labeled with a unique app label that will be used by the Ingress controller to route traffic.
An example YAML config file for the internal service is shown below:
<pre class="code-block">
yaml
apiVersion: v1
kind: Service
metadata:
  name: internal-service
  labels:
    app: internal-service
spec:
  selector:
    app: internal-service
  ports:
    - name: http
      port: 8080
      protocol: TCP
</pre>
#### How to Configure Ingress in Your Cluster?

To use Ingress, you need to have an Ingress controller running in your Kubernetes cluster. 
An Ingress controller is a component that runs as a pod and watches for changes in the Ingress resource. It then configures the load balancer accordingly.

There are several Ingress controllers available, including Nginx, Traefik, and Istio. 
Once you have chosen an Ingress controller, you can deploy it in your cluster using a deployment or a DaemonSet.

After deploying the Ingress controller, you can create an Ingress resource in your cluster to define the routing rules for incoming traffic.

#### What is Ingress Controller?

An Ingress controller is a Kubernetes component that acts as a traffic router for incoming traffic. 
It is responsible for configuring the load balancer and routing traffic to the appropriate internal service based on the Ingress resource's rules.

- Environment on Which Your Cluster is Running (Cloud Provider or Bare Metal):

The environment on which your cluster is running can affect how you configure Ingress.
If you are running your cluster on a cloud provider, you may need to use a cloud-specific load balancer, such as AWS ELB or GCP Load Balancer, 
to expose your Ingress controller to the internet.

If you are running your cluster on bare metal, you can use a software load balancer, such as Nginx or Traefik, to expose your Ingress controller to the internet.

#### Conclusion:

Ingress is a powerful tool in Kubernetes that acts as a traffic router to the internal services from external networks, 
providing advanced features like load balancing, SSL termination, and routing rules. In contrast to an external service, 
Ingress supports HTTP and HTTPS protocols and provides more functionalities. To configure Ingress in your cluster, 
you need to have an Ingress controller running in your Kubernetes cluster, 
which is responsible for configuring the load balancer and routing traffic to the appropriate internal service based on the Ingress resource's rules. 
The environment on which your cluster is running can affect how you configure Ingress, 
and different Ingress controllers are available, including Nginx, Traefik, and Istio.
