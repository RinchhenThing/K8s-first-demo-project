# MongoDB and Mongo Express on Kubernetes

## Project Overview

This project demonstrates how to deploy a simple web application and database stack on Kubernetes. The application consists of MongoDB as the database and Mongo Express as the web-based administration interface. The purpose of the project is to understand how Kubernetes resources work together to deploy and manage a complete application.

The project covers several core Kubernetes concepts, including Deployments, Services, Secrets, and ConfigMaps. It also demonstrates how applications communicate within a Kubernetes cluster and how a service can be exposed externally for user access.

---

## Project Architecture

The application is composed of two main components:

1. **MongoDB**

   * Acts as the database server.
   * Stores application data.
   * Runs inside a Kubernetes Pod managed by a Deployment.

2. **Mongo Express**

   * Provides a web-based interface for managing MongoDB.
   * Connects to MongoDB through an internal Kubernetes Service.
   * Is exposed externally through a Kubernetes Service so it can be accessed from a browser.

The communication flow is as follows:

Browser → Mongo Express Service → Mongo Express Pod → MongoDB Service → MongoDB Pod

---

## Objectives

The primary objectives of this project were:

* Learn how to deploy applications using Kubernetes Deployments.
* Understand the purpose and use of Kubernetes Services.
* Learn how Secrets are used to securely manage sensitive information.
* Understand how ConfigMaps can be used to store application configuration.
* Learn how applications communicate within a Kubernetes cluster.
* Expose an application to external users through a Kubernetes Service.

---

## Project Components

### MongoDB Deployment

The first component created was the MongoDB Deployment. The Deployment is responsible for creating and managing the MongoDB Pod. Kubernetes continuously monitors the Pod and recreates it if it fails, ensuring that the database remains available.

Labels and selectors were used to allow other Kubernetes resources to identify and communicate with the MongoDB Pod.

---

### Kubernetes Secret

MongoDB requires authentication credentials, such as a username and password. Rather than storing these credentials directly in deployment files, a Kubernetes Secret was created.

The Secret stores sensitive information securely and allows the Deployment to retrieve the values when creating the MongoDB container.

Using Secrets provides better security and follows Kubernetes best practices.

---

### MongoDB Internal Service

Pods receive dynamic IP addresses that may change whenever a Pod is recreated. To provide a stable way for other applications to access MongoDB, an internal Service was created.

The Service acts as a permanent endpoint for MongoDB within the cluster. Applications no longer need to know the Pod’s IP address and can instead communicate using the Service name.

This enables reliable communication between Mongo Express and MongoDB.

---

### ConfigMap

Mongo Express needs information about the MongoDB server location. Instead of hardcoding this information inside the application configuration, a ConfigMap was created.

The ConfigMap stores non-sensitive configuration data, making it easier to manage and update configuration values without modifying application deployments.

This approach improves maintainability and follows Kubernetes configuration management practices.

---

### Mongo Express Deployment

The Mongo Express Deployment creates and manages the Mongo Express Pod.

The Deployment retrieves:

* MongoDB credentials from the Secret.
* MongoDB connection information from the ConfigMap.

This allows Mongo Express to securely connect to MongoDB while keeping configuration centralized and manageable.

---

### Mongo Express External Service

To allow users to access Mongo Express from a web browser, an external Service was created.

The Service exposes the Mongo Express application outside the Kubernetes cluster. Users can connect to the Service and access the Mongo Express web interface without needing direct access to the Pod.

This demonstrates how Kubernetes can make applications available to external clients.

---

## Key Kubernetes Concepts Demonstrated

### Deployments

Deployments manage the lifecycle of Pods. They ensure the desired number of replicas are running and automatically recover from failures.

### Pods

Pods are the smallest deployable units in Kubernetes and contain the running application containers.

### Labels and Selectors

Labels provide metadata for resources, while selectors allow Deployments and Services to identify the resources they should manage or communicate with.

### Services

Services provide stable networking endpoints and enable communication between applications running inside the cluster.

### Secrets

Secrets securely store sensitive information such as usernames, passwords, and tokens.

### ConfigMaps

ConfigMaps store non-sensitive configuration values and allow applications to retrieve configuration without hardcoding values.

---

## Skills and Knowledge Gained

Through this project, I gained practical experience with:

* Creating and managing Kubernetes Deployments.
* Understanding how Pods are created and maintained.
* Using labels and selectors to connect Kubernetes resources.
* Configuring internal communication using Services.
* Managing sensitive information with Secrets.
* Managing application configuration with ConfigMaps.
* Exposing applications externally through Kubernetes Services.
* Troubleshooting Kubernetes resources using kubectl commands.

---

## Conclusion

This project provided a practical introduction to deploying multi-component applications on Kubernetes. By deploying MongoDB and Mongo Express, I learned how different Kubernetes resources work together to create a secure, scalable, and manageable application environment.

The project reinforced fundamental Kubernetes concepts such as Deployments, Services, Secrets, ConfigMaps, networking, and application exposure, providing a strong foundation for more advanced Kubernetes workloads and cloud-native applications.
