# Kubernetes YAML Configuration File
Kubernetes is an open-source container orchestration platform that allows you to deploy, manage, and scale containerized applications. 
Kubernetes uses YAML configuration files to define the desired state of your application. 
In this report, we will explore the key components of a Kubernetes YAML configuration file, including metadata, specification, and status. 
We will also examine the format of the configuration file, the blueprint for pods, and how to connect services to deployments and pods using labels, selectors, 
and ports.

# 3 Parts of a Kubernetes Configuration File:
A Kubernetes configuration file consists of three main parts: 

1. Metadata:
The metadata section of a Kubernetes configuration file includes information about the object being defined, such as its name, namespace, and labels.

2. Specification:
The specification section of a Kubernetes configuration file defines the desired state of the object being created, such as the container image, command, and arguments.

3. Status:
The status section of a Kubernetes configuration file provides information about the current state of the object, such as the number of replicas and their current status.

# Format of Configuration File:
The format of a Kubernetes configuration file is YAML, which stands for "YAML Ain't Markup Language". YAML is a human-readable data serialization language that is commonly used for configuration files. The syntax of a YAML file consists of key-value pairs, and indentation is used to represent nested objects.

# Blueprint for Pods (Template):
The blueprint for pods is defined in the specification section of the Kubernetes configuration file using a template. 
The template includes information about the container image, command, arguments, and environment variables. 
The template also includes the resources needed by the container, such as CPU and memory limits. 

# Connecting Services to Deployments and Pods (Label, Selector, and Port):
To connect services to deployments and pods, you can use labels, selectors, and ports.

1. Labels:
Labels are key-value pairs that are used to identify objects. 
You can add labels to deployments, pods, and services to identify which pods belong to which deployments and services.

2. Selector:
Selectors are used to match labels in a deployment or pod to labels in a service. The selector ensures that the service is connected to the correct pods.

3. Port:
Ports are used to specify the port number that the service should listen on. The port is used to route traffic to the correct pod.







