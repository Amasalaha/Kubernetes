## Demo: Configure Ingress in Minikube

#### Introduction:
In this demo, we will configure Ingress in Minikube, which is a popular tool for local Kubernetes development. 
Ingress is a Kubernetes object that allows external access to services in a cluster. 
We will explore the following topics in this demo: Ingress Default Backend, Routing Use Cases, and Configuring TLS Certificate.

##### Ingress Default Backend:
Ingress Default Backend is a service that handles requests that do not match any other Ingress rules. 
In other words, if a user requests a URL that is not defined in the Ingress rules, the request will be directed to the default backend. 
In this demo, we will create a default backend service using the following command:
<pre class="code-block">

$ kubectl create deployment httpenv --image=bretfisher/httpenv
</pre>
- Routing Use Cases:

Routing is the process of directing incoming network traffic to different endpoints based on the URL. 
In this demo, we will create two services, "foo" and "bar," and define the routing rules using Ingress. 
We will also create a host-based routing rule that directs traffic to different services based on the hostname. 
We will use the following commands to create the services and Ingress rules:
<pre class="code-block">

$ kubectl create deployment foo --image=k8s.gcr.io/echoserver:1.10
$ kubectl create service clusterip foo --tcp=8080
$ kubectl create deployment bar --image=k8s.gcr.io/echoserver:1.10
$ kubectl create service clusterip bar --tcp=8080
$ kubectl apply -f ingress.yaml
</pre>
- Configuring TLS Certificate:

TLS (Transport Layer Security) is a protocol that provides secure communication over the internet.
In this demo, we will configure a TLS certificate for the Ingress controller using the following steps:

Create a self-signed certificate:
<pre class="code-block">

$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=nginxsvc/O=mycompany"
</pre>
Create a Kubernetes secret:
<pre class="code-block">

$ kubectl create secret tls tls-secret --key tls.key --cert tls.crt
</pre>
Update the Ingress rule to use the TLS certificate:
<pre class="code-block">

spec:
tls:

secretName: tls-secret
hosts:
mycompany.com
</pre>
#### Conclusion:
In this demo, we learned how to configure Ingress in Minikube and explored different routing use cases. 
We also learned how to configure a TLS certificate for the Ingress controller to provide secure communication over the internet.
Ingress is an essential Kubernetes object that provides external access to services in a cluster, 
and understanding its configuration is crucial for Kubernetes developers.
