# Cloud Computing Lab - Artifact Registries and Serverless Computing Platforms
Researched and compared artifact registries and serverless computing platforms in AWS, GCP, and Azure. 

# Task 1: Artifact Registries Research
Identified the most popular artifact registries in AWS, GCP, and Azure.

## Artifact Registries
Artifact registries are centralized repositories that store and manage software packages, container images, and other artifacts used in development and deployment processes. They enable teams to share and distribute artifacts, ensuring consistency and security throughout the development lifecycle.

### AWS
#### 1. [AWS CodeArtifact](https://aws.amazon.com/codeartifact/)
AWS CodeArtifact is a secure, scalable, and cost-effective artifact management service for software development.

##### Key Features:
- **Fully Managed Service**: CodeArtifact simplifies the process of storing, publishing, and sharing software packages, allowing organizations to focus on development without managing infrastructure.
- **Integration with Public Repositories**: Easily consume packages from public artifact repositories like npm, Maven Central, PyPI, RubyGems.org, and NuGet.org with quick configuration.
- **High Availability and Durability**: CodeArtifact operates across multiple Availability Zones and securely stores data in Amazon S3 and Amazon DynamoDB, ensuring high availability and durability.
- **Access Control and Monitoring**: Leverage AWS IAM for fine-grained access control, and monitor package access with CloudTrail and AWS Key Management Service (KMS) for encryption.
- **Pricing:** With AWS CodeArtifact, there are no upfront fees or commitments. You pay only for what you use: the size of the artifacts stored, the number of requests made, and the amount of data transferred out of an AWS Region. CodeArtifact includes a monthly AWS Free Tier for storage and requests.
- [more concrete description of features](https://aws.amazon.com/codeartifact/features/)

### GCP
#### 1. [Google Artifact Registry](https://cloud.google.com/artifact-registry/docs)
Google Artifact Registry is a platform that allows you to seamlessly manage container images, integrate with Cloud Build and third-party CI/CD systems.

##### Key Features:
- **Centralized Artifact Management**: Provides a single location for storing and managing your packages and Docker container images.
- **CI/CD Integration**: Seamlessly integrate with Google Cloud CI/CD services or your existing CI/CD tools to streamline your workflow.
- **Deployment Support**: Deploy artifacts to various Google Cloud runtimes, including Google Kubernetes Engine, Cloud Run, Compute Engine, and App Engine flexible environment.
- **Identity and Access Management**: Utilize consistent credentials and access control to manage who can access your artifacts.
- **Container Metadata Management**: Manage container metadata and scan for vulnerabilities with Artifact Analysis for enhanced security.
- **Regional Repositories**: Create multiple regional repositories within a single Google Cloud project to group images by team or development stage, controlling access at the repository level.
- [more concrete description of features](https://cloud.google.com/artifact-registry/docs/overview)

### Azure
#### 1. [Azure Artifacts](https://azure.microsoft.com/en-us/products/devops/artifacts)
Azure Artifacts is a cloud-based package management service that allows developers to create, host, and share packages across multiple programming languages while integrating seamlessly with Azure DevOps for efficient CI/CD workflows.

##### Key Features:
- **Multi-language Package Feeds**: Create and share package feeds for Maven, npm, NuGet, Python, and Rust from both public and private sources.
- **Seamless CI/CD Integration**: Enhance your continuous integration/continuous delivery (CI/CD) pipelines with fully integrated package management available with a single click.
- **Efficient Code Sharing**: Easily share code across small teams and large enterprises, fostering collaboration and productivity.
- **Universal Artifact Management**: Manage all package types, providing universal artifact management for Maven, npm, NuGet, and Python.
- **Flexible Pipeline Integration**: Add packages to any pipeline, enabling sharing, built-in CI/CD capabilities, versioning, and testing for streamlined development workflows.


## Task 2: Serverless Computing Platform Research
Identified the best serverless computing platforms in AWS, GCP, and Azure.

### Serverless computing
Serverless computing allows developers to run applications without managing server infrastructure, as the cloud provider handles the backend on-demand and charges based on a pay-as-you-go model. Despite the name, servers still exist; they are managed by the provider, freeing developers to focus on front-end code and logic. Resources are allocated when a function is executed and released when it stops, optimizing operational costs by avoiding charges for idle resources. Benefits include the elimination of capacity planning, reduced administrative burdens, high availability, disaster recovery, and auto-scaling capabilities. Billing is granular, measured in increments of 100 milliseconds, ensuring efficient resource utilization. [(source)](https://dev.to/clickit_devops/fargate-vs-lambda-the-battle-of-the-future-pkk)

### AWS 
#### 1. AWS Lambda
AWS Lambda is an event-driven, pay-as-you-go compute service that lets you run code without provisioning or managing servers.[(source)](https://aws.amazon.com/serverless/)

##### [Key features:](https://aws.amazon.com/lambda/)
- **No need for managing servers:** Run code without provisioning or managing infrastructure. Simply write and upload code as a .zip file or container image.
- **Automatic scaling:** Automatically respond to code execution requests at any scale, from a dozen events per day to hundreds of thousands per second.
- **Pay-as-you-go pricing:** Save costs by paying only for the compute time you use—by the millisecond—instead of provisioning infrastructure upfront for peak capacity.
- **Performance optimization:** Optimize code execution time and performance with the right function memory size. Respond to high demand in double-digit milliseconds with Provisioned Concurrency.
- **Supported Languages:** Supports a wide range of languages
- **Integration:** Integrated with other AWS services
- [more concrete description of features](https://aws.amazon.com/lambda/features/)
- [has useful price calculator](https://calculator.aws/#/createCalculator/Lambda)

#### 2. AWS Fargate
AWS Fargate is a serverless compute engine that works with Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS).

##### [Key features:](https://aws.amazon.com/fargate/)
- **Application Management:** Eliminates operational overhead for server management.
- **Integrated Monitoring:** Provides metrics and insights through AWS services like CloudWatch Container Insights.
- **Workload Isolation:** Ensures security with dedicated runtime environments.
- **Cost Optimization:** Charges only for compute resources used, with options for Savings Plans, Fargate Spot, or AWS 
- [more concrete description of features](https://aws.amazon.com/fargate/features/)
- [also has very useful calculator](https://calculator.aws/#/createCalculator/Fargate)

### GCP
GCP's serverless offerings — Cloud Run, App Engine, and Cloud Functions — provide a range of options to build and deploy applications that automatically scale with demand, allowing developers to focus on writing code rather than managing infrastructure. [source](https://medium.com/@williamwarley/gcp-serverless-stack-guide-cloud-run-appengine-cloud-function-b890930650f1)

#### 1. Cloud Run
A managed compute platform that enables you to run stateless containers that are invocable via HTTP requests. Cloud provide a portable and open API and runtime environment for your services.

##### Key Features:
- **Scalability:** Automatically scales applications based on incoming requests or events, even down to zero when idle.
- **Fully Managed:** Manages all infrastructure aspects, including provisioning, scaling, and networking.
- **Event-Driven Architecture:** Integrates with Pub/Sub for real-time event processing and Cloud Storage for file triggers.
- **Flexibility:** Supports any language or library that can be containerized, offering high deployment flexibility.
- **Integration with GCP Services:** Connects seamlessly with services like Firestore, BigQuery, and Cloud SQL for dynamic and complex applications.

#### 2. App Engine
A Platform as a Service (PaaS) offering that abstracts away infrastructure so you can focus on code. App Engine automatically scales your app up and down while balancing the load. It supports popular languages such as Node.js, Python, Java, Ruby, C, Go, PHP, and more.

##### Key Features:
- **Automatic Scaling:** Dynamically scales applications based on traffic demands, ensuring optimal performance.
- **Two Environments:** Offers a Standard environment for lightweight apps and a Flexible environment for more control and custom runtimes.
- **Seamless GCP Integration:** Easily connects with other GCP services like Cloud Datastore, Cloud SQL, and Cloud Pub/Sub for enhanced functionality.
- **Focus on Development:** Allows developers to concentrate on coding without worrying about infrastructure management.
- **API and Microservices Support:** Ideal for hosting web applications, API backends, and microservices as part of a larger ecosystem.

#### 3. Cloud Functions
A lightweight compute solution for developers to create single-purpose, stand-alone functions that respond to cloud events without the need for managing a server or runtime environment. Cloud Functions can be triggered by events from within GCP services like Cloud Storage, Pub/Sub, and Firestore, or from HTTP requests.

##### Key Features:
- **Event-Driven Execution:** Functions are triggered by specific events from GCP services or HTTP requests, allowing for responsive processing.
- **Stateless Functions:** Each function invocation runs in its instance, enabling automatic scaling from a few to millions of invocations based on demand.
- **Fully Managed Environment:** Handles all aspects of function execution, including provisioning, scaling, and monitoring, without developer intervention.
- **Integration with GCP Services:** Seamlessly integrates with services like Cloud Storage, Firestore, and Pub/Sub for sophisticated workflows and data processing.
- **Flexible Deployment:** Functions can be easily deployed and configured using Infrastructure as Code (IaC) tools like Terraform.

#### Azure
#### 1. Azure Functions
Azure Functions is a serverless compute service that allows developers to run event-driven code without managing infrastructure. It enables the creation of scalable applications using a variety of programming languages while focusing on business logic.

##### Key Features:
- **Flexible Development:** Supports multiple programming languages and simplifies integration with Azure services.
- **Versatile Use Cases:** Ideal for intelligent apps, real-time processing, and workflow orchestration.
- **Built-in Security and Compliance:** Strong cybersecurity measures and extensive compliance certification portfolio.
- **Flexible Pricing Options:** Offers various plans, including a consumption plan and premium options for scaling.
- **Integration with Azure Services:** Works seamlessly with other Azure products like Azure Container Apps and Azure OpenAI Service.

#### 2. Azure Container Apps
Azure Container Apps is a fully managed serverless container platform designed for building and deploying cloud-native applications and microservices. It enables developers to focus on writing code without the complexities of managing infrastructure.

##### Key Features:
- **Fully Managed Platform:** Reduces operational management overhead by hosting modern apps without needing to configure complex infrastructure.
- **On-Demand Scaling:** Automatically scales applications based on demand, enhancing production velocity while lowering management costs.
- **Open-Source Foundation:** Integrates with Distributed Apps Runtime (Dapr) and Kubernetes Event-driven Autoscaling (KEDA) for improved app lifecycle management.
- **Advanced Networking:** Supports flexible network architecture with Virtual Network (VNet) integration and detailed ingress and egress controls.
- **Enhanced Security and Governance:** Monitors governance at scale with advanced identity and access management features.
- **Multi-Environment Deployment:** Allows users to host applications from the cloud to the edge with Azure Arc, providing flexibility in deployment.
- **Trial period:** 12 months of free services

#### 3. Azure App Service
Azure App Service is a fully managed platform as a service (PaaS) that enables developers to quickly build, deploy, and scale web applications and APIs globally. This service allows teams to focus on application development without the complexities of infrastructure management.

##### Key Features:
- **Multi-Language Support:** Supports popular programming languages including ASP.NET, Java, Node.js, PHP, and Python on both Windows and Linux.
- **Automated Deployment:** Features automatic scaling and workload management, simplifying deployment processes.
- **Zero Trust Security:** Implements built-in authentication and authorization features to ensure secure access.
- **High Availability:** Guarantees a 99.95% uptime SLA, enhancing app resilience during outages.
- **Comprehensive Compliance:** Meets various enterprise security and compliance standards through actively secured platform components.
- **Containerization Support:** Allows users to containerize applications and host them in a custom environment.
- **Pricing:** Provides a wide range of flexible and cost-effective plans.
