# Cloud Native Web Application 

## Technologies Used : 
Java Spring boot, MySQL, Packer, Google Cloud Platform (GCP), Terraform, GitHub CI/CD

## Project Desceription:
This project encompasses the development of a cloud-native web application leveraging a microservices architecture. Utilizing cutting-edge technologies such as Java Spring Boot and MySQL database at the backend, aimed to deliver a robust and scalable solution.

## Key Features and Technologies:
### Java Spring Boot: 
The backend of our application is built on Java Spring Boot framework, offering rapid development and seamless integration capabilities.

### MySQL Database: 
For data storage and management, integrated MySQL database, ensuring reliability and performance.

### Infrastructure Automation with Terraform:
To streamline deployment and management of our application infrastructure on Google Cloud Platform (GCP), provisioned Terraform templates. These templates automate the setup of essential components such as Virtual Private Cloud (VPC), Subnets, Internet Gateway, Compute Engine Instances (VMs), and Load Balancers, ensuring high availability and scalability.

### CI/CD Pipeline with GitHub Actions:
Established a robust CI/CD pipeline using GitHub Actions. This pipeline automates the build, test, and deployment processes. It triggers Packer Custom Image builder to create custom images and initiates Code Deploy actions for seamless deployment of updates.

## Project Goals:
### Scalability: 
Leverages microservices architecture and cloud infrastructure, to ensure that the application scales effortlessly to meet increasing demands and user loads.

### Reliability:
Prioritizes reliability of our application by implementing high availability measures such as load balancing and redundancy in the infrastructure setup.

### Automation:
Aimed to minimize manual intervention, enhance efficiency, and accelerate the delivery of new features and updates, through infrastructure automation and CI/CD pipeline.


## Build Instructions: 
1. Clone this repository into the local system 
2. Open the CLI 
3. To build the application:
> mvn clean install 
4. To run the application:
> mvn spring-boot:run

## Implemented Features:
1. Health Check Endpoint: Implemented an endpoint /healthz that checks connectivity to the database. It returns HTTP 200 OK if the connection is successful and HTTP 503 Service Unavailable if the connection fails.

2. User APIs: Added APIs for creating, updating, and retrieving user details.
GET Endpoint- /v1/user/self
POST Endpoint-v1/user
PUT Endpoint-v1/user/self

3. Integration tests: Implemented Integration tests for the /v1/user endpoint with a new GitHub Actions workflow. 
Test 1 - Created an account, and using the GET call, validated account exists.
Test 2 - Updated the account and using the GET call, validated the account was updated.

## Packer & Custom Images - Building Custom Application Images using Packer
Created custom application images for deployment in Google Cloud Platform (GCP) using Packer. These custom images are tailored to include all necessary dependencies and configurations required to run our application.

### Packer Pre-requisites
1. Install Packer on MacOS:
> brew tap hashicorp/tap
> brew install hashicorp/tap/packer
2. Install packer plugins
> packer plugins install github.com/hashicorp/googlecompute
3. Create new project in gcp and enable Compute Engine API
4. Create a custom service account for Packer and assign it Compute Instance Admin (v1) & Service Account User roles.
5. Add above GCP Credentials, DB Username, url and password in github repo secrets  
6. Provide project id in main packer file 

### Custom Image Implementation
1. Source Image: Centos Stream 8
2. Local Installation: MySQL is installed in the custom image.
3. Application Inclusion: Custom images includes everything needed to run web application and the application binary itself.
4. Created a local user csye6225 with primary group csye6225. This user will not have a login shell. Ensured that the application artifacts and configurations are owned by user csye6225 and group csye6225.
5. Added the systemd service file to /etc/systemd/system and configured it to start the service when the instance is launched.




