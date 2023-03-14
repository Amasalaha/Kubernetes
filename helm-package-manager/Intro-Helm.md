<details>
 <summary><h3></a> <a href="https://helm.sh/" target="_blank" rel="noreferrer">
<img src="https://cncf-branding.netlify.app/img/projects/helm/horizontal/color/helm-horizontal-color.png" alt="helm" width="100" height="100"/></h3></summary>
Helm is a popular package manager for Kubernetes, it simplifies the installation and management of Kubernetes applications.
It has become a crucial tool for DevOps engineers, Kubernetes administrators and developers as it allows them to define, 
install and manage their applications using a single file called a Helm chart. This report will provide an overview of Helm, 
including its package manager and chart structure, as well as its templating engine, use cases, and values injection into template files. 
Additionally, it will discuss the Tiller release management system that was present in Helm version 2.

#### Package Manager and Helm Charts:
Helm is a package manager for Kubernetes, similar to apt for Debian and Ubuntu, yum for CentOS and Fedora, and Homebrew for macOS. 
It allows users to define, install, and upgrade their Kubernetes applications in a simple and streamlined way.

Helm charts are the packaged form of Kubernetes applications that can be installed and deployed with Helm. 
A chart is a collection of files that describe a related set of Kubernetes resources, including deployments, services, ingress rules, and more.

#### Templating Engine:
One of the most powerful features of Helm is its templating engine. The templating engine allows users to define variables that can be used to parameterize a chart. 
These variables can be used to create multiple versions of the same chart, customized for different environments.

For example, you can define variables for environment-specific values, such as the number of replicas for a deployment, 
or the size of a persistent volume claim. When the chart is installed, the variables are replaced with their corresponding values,
making it easy to deploy the same application to multiple environments with different configurations.

- Use Cases for Helm:

Helm can be used in a variety of scenarios, including:

1. Application deployment: Helm makes it easy to deploy and manage Kubernetes applications, 
allowing DevOps engineers to focus on their core tasks rather than spending time on application deployment.

2. Continuous Integration/Continuous Deployment (CI/CD): Helm can be integrated into CI/CD pipelines,
allowing for automated testing and deployment of Kubernetes applications.

3. Infrastructure as Code: Helm allows users to define their infrastructure as code, enabling version control, collaboration, and auditability.

#### Helm Chart Structure:
A Helm chart is made up of several components, including:

- Chart.yaml: This file contains metadata about the chart, including its name, version, and description.

- Values.yaml: This file contains the default values for the chart's variables.

- templates/: This directory contains the template files that are used to generate the Kubernetes resources.

- charts/: This directory can be used to include other charts as dependencies.

#### Values Injection into Template Files:
Helm's templating engine allows users to define variables that can be used to parameterize a chart. 
These variables can be used in the template files to generate Kubernetes resources.

For example, if you have a variable called "replicas" defined in your values.yaml file, you can use it in the template file for a deployment like this:
<pre class="code-block">
yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: {{ .Values.replicas }}
  template:
    ...
 </pre>
When the chart is installed, Helm will replace {{ .Values.replicas }} with the value defined in values.yaml.

#### Release Management / Tiller (Helm Version 2!):
Helm version 2 included a component called Tiller, which was responsible for managing releases of Helm charts. 
Tiller would install the chart on the Kubernetes cluster and maintain a record of the installed chart's configuration.

Tiller was a security risk because it ran with administrative privileges and had access to the entire Kubernetes cluster. 
In Helm version 3, Tiller was removed, and the responsibility for managing
