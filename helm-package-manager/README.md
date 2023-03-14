<details>
 <summary><h3> Demo Report :  </h3></summary>

Helm is a popular package manager for Kubernetes, which makes it easy to install, manage, and upgrade complex applications on Kubernetes clusters. 
In this demo report, we will demonstrate how to use Helm to deploy and manage a sample application on a Kubernetes cluster.

#### Prerequisites
Before we begin, make sure you have the following tools installed:

- Kubernetes cluster
- Helm
We assume that you already have a running Kubernetes cluster and Helm installed on your system.

#### Demo
For this demo, we will deploy the popular "WordPress" application using Helm. WordPress is a content management system that allows users to create and manage websites. To deploy WordPress using Helm, we need to follow these steps:

Add the official WordPress chart repository to Helm:

<pre class="code-block">
bash
helm repo add bitnami https://charts.bitnami.com/bitnami
</pre>

Update the local Helm chart repository cache:

<pre class="code-block">
bash
helm repo update
</pre>

Install the WordPress chart using Helm:

<pre class="code-block">
bash
helm install my-wordpress bitnami/wordpress
</pre>

This command will deploy the WordPress application on your Kubernetes cluster using the default configuration settings provided by the Helm chart.
Verify that WordPress has been deployed successfully by running the following command:

<pre class="code-block">
bash
kubectl get pods
</pre>

You should see one or more pods running the WordPress application.
Access the WordPress application by running the following command:

<pre class="code-block">
bash
kubectl port-forward svc/my-wordpress 8080:80
</pre>

This command will forward the port 80 of the my-wordpress service to port 8080 on your local machine. 
You can now access the WordPress application by opening a web browser and navigating to http://localhost:8080.

To upgrade WordPress to a newer version, run the following command:
<pre class="code-block">
bash
helm upgrade my-wordpress bitnami/wordpress
</pre>

This command will upgrade the WordPress application to the latest version available in the Helm chart repository.
To uninstall WordPress, run the following command:

<pre class="code-block">
bash
helm uninstall my-wordpress
</pre>

This command will remove the WordPress application from your Kubernetes cluster.

#### Conclusion
In this demo report, we demonstrated how to use Helm to deploy and manage a sample application on a Kubernetes cluster. 
Helm makes it easy to install, manage, and upgrade complex applications on Kubernetes clusters, and it is widely used in the Kubernetes community.
