# Deployment of a Micrservice-based Application (Sockshop) on Kubernetes using modern approach

### Objective:
> Our aim is to deploy a microservices-based application, specifically the Socks Shop, using a modern approach that emphasizes automation and efficiency. The goal is to use Infrastructure as Code (IaaC) for rapid and reliable deployment on Kubernetes.

#### Project Overview
The Socks Shop application is a widely recognized microservices-based e-commerce platform, often utilized as a reference for showcasing modern cloud-native technologies. This application is composed of several microservices, each dedicated to a specific function such as product catalog, shopping cart, and user authentication. Designed with scalability, resilience, and fault tolerance in mind, the Socks Shop application is an ideal candidate for deployment on Kubernetes.

This project focuses on deploying the Socks Shop application on a Kubernetes cluster using an Infrastructure as Code (IaC) approach.

##### Prerequisites
To successfully complete this project, the following tools and services are required:

Terraform : For provisioning infrastructure resources on AWS.
Azure Account : To host the cloud infrastructure, including the Kubernetes cluster.
Kubernetes : For container orchestration, managing the deployment and scaling of microservices.
Helm : For managing Kubernetes applications as Helm charts.
Prometheus : For monitoring the performance and health of the application and infrastructure.
ELK Stack (Elasticsearch, Logstash, Kibana) : For logging, centralizing, and visualizing logs from the microservices.
Let's Encrypt : For securing the application with SSL/TLS certificates.
Socks Shop Application : The microservices-based e-commerce platform being deployed.
Infrastructure Provisioning
Using Terraform, we will provision the necessary infrastructure resources on Azure. This approach ensures a clear and reproducible infrastructure setup.
