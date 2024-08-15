# Deployment of a Microservice-based Application (Sockshop) on Kubernetes using modern approach

### Objective:
> Our aim is to deploy a microservices-based application, specifically the Socks Shop, using a modern approach that emphasizes automation and efficiency. The goal is to use Infrastructure as Code (IaaC) for rapid and reliable deployment on Kubernetes.

#### Project Overview
The Socks Shop application is a widely recognized microservices-based e-commerce platform, often utilized as a reference for showcasing modern cloud-native technologies. This application is composed of several microservices, each dedicated to a specific function such as product catalog, shopping cart, and user authentication. Designed with scalability, resilience, and fault tolerance in mind, the Socks Shop application is an ideal candidate for deployment on Kubernetes.

This project focuses on deploying the Socks Shop application on a Kubernetes cluster using an Infrastructure as Code (IaC) approach.

#### Prerequisites
To successfully complete this project, the following tools and services are required:

- Terraform : For provisioning infrastructure resources on Azure.
- Azure Account : To host the cloud infrastructure, including the Kubernetes cluster.
- Kubernetes : For container orchestration, managing the deployment and scaling of microservices.
- Helm : For managing Kubernetes applications as Helm charts.
Socks Shop Application : The microservices-based e-commerce platform being deployed.

> Infrastructure Provisioning
Using Terraform, we will provision the necessary infrastructure resources on Azure. This approach ensures a clear and reproducible infrastructure setup.

### SetUp and Initialization
 **STEP 1**

 The goal is to initialzile, plan and apply terraform in your working directory having configured all the necessary *.tf* files required for the provisioning the necessary resources and Kubernetes cluster on Azure. 

After creating and configuring the following terraform files *providers.tf, ssh.tf , main.tf, variables.tf, outputs.tf.* 

You run the following commands to initialize and set up Kubernertes cluster on Azure using terraform `terraform init --upgrade`,  

`terraform plan -out main.tf.plan`, 

`terraform apply main.tf.plan`

![k8setup](.\images\01_terraformapply.png)

**STEP 2**

Once we've applied our terraform and all required resources have been added, we need to check that the health of the cluster with the command `kubectl get nodes` thereafter checking to confirm the active namespaces on thr cluster created using the command `kubectl getnamespace`.

![kubectlcheck](./images/02_namespacecheck.png)

**STEP 3**

We were given this link *https://github.com/microservices-demo/microservices-demo/tree/master* to provision the sockshop microservice application and we'd use the yaml file deploy.

![kubectlsockshop](./images/03_kubectlsockshop.png)

After successfully deploying the application, we'd need to be sure the application is running smoothly by using the command `kubectl get pods,svc -sockshop.yaml`. This command simply lists all available pods and services in the specified namespace which in this case is sockshop.yaml.

![kubectlpods](./images/04_kubectlgetpods.png)

**STEP 4**

Now it's important we install an ingress controller which helps to route traffic to our pods and is also useful for accessing our applicaton through an external ip. 

We'd use the command `helm search repo nginx` after adding th repo. 

![helmrepo](./images/05_helmnginx.png)

After figuring out the exact name of the ingress to install, we use he command `helm install wizingress nginx/nginx-ingress`. The *wizingress* in the command is my personal name i decided to name the ingress.

![helmwizingress](./images/06_helmwizingress.png)

Thereafter, simply check for successful installation of the service using `kubectl get pods,svc` and you should see the newly installed ingress controller alongsides other running pods and services.

![kubectlsvcpods](./images/07_kubectlgetsvc.png)

You should also note that the ingess has an External I.P 40.78.82.178 which can be accessible through port 80 and would serve the frontend of our application.

We do not intend to view our application via i.p address as that's not a best practice so we'd be mapping this same external ip created by ingress to our designated domain name.

**STEP 5**
Using namecheap.com, we update our domain name *(wisdomgoddy.me)* to point to the ip gotten from nginx-ingress so that our application can be accessible through the domain name we mapped the external ip.

![namecheapdns](./images/08_namecheapdns.png)

**STEP 6**
In this step all we need to do is view our application that's mapped to the dommain name on our web browser.

![sockshopinsecure](./images/10_sockshopinsecure.png)

The application's frontend is good to go and successfully mapped to our domain name but you'd also note that the connection is insecure.

**STEP 7**

