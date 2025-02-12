# Terraform

### What is Terraform? What is it used for?
* Terraform is used to automate the provisioning, management, and scaling of infrastructure across multiple cloud providers and on-premise data centers. Some common use cases include:
  * Cloud Infrastructure Provisioning – Deploy resources on AWS, Azure, Google Cloud, etc.
  * Multi-Cloud and Hybrid Cloud Management – Manage infrastructure across multiple cloud providers from a single tool.
  * Infrastructure Automation – Define, version, and deploy infrastructure in a consistent and repeatable way.
  * Configuration as Code – Store infrastructure configurations in version control (e.g., Git).
  * Scalability and Efficiency – Automatically scale infrastructure up or down as needed.
  * Security and Compliance – Use policy-as-code tools like Sentinel to enforce security policies.

### Why use Terraform? The benefits?
* Terraform is widely used because it provides a declarative, efficient, and scalable way to manage infrastructure. Here are some key benefits:
  * Allows infrastructure to be defined in code, making it repeatable, version-controlled, and consistent.
  * Easily collaborate with teams using version control systems like Git.
  * Works across multiple cloud providers (AWS, Azure, Google Cloud, Kubernetes, etc.) and on-premise infrastructure.
  * Uses parallel execution, meaning Terraform can deploy multiple resources simultaneously.

### Alternatives to Terraform
* Pulumi
* AWS CloudFormation

### Who is using Terraform in the industry?
* Terraform is widely adopted across industries, particularly by companies with large-scale infrastructure needs, cloud-based services, and DevOps practices.
* Tech Giants & Cloud Providers (Netflix, Amazon, Uber)
* Financial Services & Banking (JPMorgan Chase )

### In IaC, what is orchestration? How does Terraform act as "orchestrator"?
* Orchestration in the context of Infrastructure as Code (IaC) refers to the process of automating the configuration, management, and coordination of multiple infrastructure resources across a network or environment. It's about ensuring all components work together as intended, whether they're virtual machines, databases, networks, or other services.

### What is best practice to supply AWS credentials?
* Environment Variables
* AWS Shared Credentials File (~/.aws/credentials)
* AWS Configuration File (~/.aws/config)
* EC2 Instance Metadata (IAM Role)


### Terraform commands
### Non-destructive
* terraform init
* terraform plan
* terraform fmt
### Destructive
* terraform apply
* terraform destroy


## Creating an 2 tier Architecture in Azure
### Steps to create
1. Provider block setup
2. Variables for RG and region
3. Define VNET and subnet
4. Create a publiv ip for the public VM - make sure to put static as 'allocation method'
5. Make a NIC
6. Reference the key you want to use
7. Make VM
8. Add key you referenced
9. Add disk
10. Add source image - make sure to define the image using a data block to define and then specify source image id

