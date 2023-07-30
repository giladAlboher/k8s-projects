# README - WordPress and MySQL Deployment on Kubernetes

This repository contains Kubernetes manifests to deploy WordPress and MySQL services on a Kubernetes cluster. The deployment consists of a WordPress application, a MySQL database, and necessary services to expose these applications.

## Prerequisites

Before deploying this application, ensure you have the following prerequisites:

1. A running Kubernetes cluster.
2. `kubectl` command-line tool installed and configured to access your cluster.

## Deployment

To deploy the WordPress and MySQL services, follow the steps below:

1. Clone this repository:

```bash
git clone <repository_url>
cd <repository_name>
```

2. Deploy MySQL service and persistent volume claim:

```bash
kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml
kubectl apply -f mysql-pvc.yaml
```

3. Deploy WordPress service:

```bash
kubectl apply -f wordpress-deployment.yaml
kubectl apply -f wordpress-service.yaml
```

4. Set up Ingress (Assuming you have an Ingress Controller like NGINX Ingress installed):

```bash
kubectl apply -f ingress.yaml
```

## Accessing the WordPress Application

After the deployment is successful, you can access the WordPress application using the Ingress URL.

For example, if your cluster's Ingress IP is `192.168.1.100` and the Ingress rule path is `/testpath`, you can access the WordPress application at:

```
http://192.168.1.100/testpath
```

## Configuration

### WordPress Deployment

The WordPress deployment uses the latest WordPress image and connects to the MySQL database using the environment variables `WORDPRESS_DB_HOST`, `WORDPRESS_DB_USER`, `WORDPRESS_DB_PASSWORD`, and `WORDPRESS_DB_NAME`.

### MySQL Deployment

The MySQL deployment uses the latest MySQL image and sets the environment variables `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, and `MYSQL_PASSWORD`.

### Persistent Volume Claim

A Persistent Volume Claim is used to provide persistent storage to the MySQL database.

### Ingress

The Ingress resource is used to route incoming requests to the WordPress service based on the specified path.

## Clean Up

To remove the deployed resources, run the following commands:

```bash
kubectl delete -f ingress.yaml
kubectl delete -f wordpress-service.yaml
kubectl delete -f wordpress-deployment.yaml
kubectl delete -f mysql-pvc.yaml
kubectl delete -f mysql-service.yaml
kubectl delete -f mysql-deployment.yaml
```

Please ensure you back up any important data before running the clean-up commands.

## Disclaimer

This deployment is intended for testing and development purposes. In a production environment, make sure to secure the services properly and follow best practices.

## Contributing

If you find any issues with the deployment or want to contribute to the repository, feel free to open a pull request or an issue. Your feedback and contributions are appreciated!
