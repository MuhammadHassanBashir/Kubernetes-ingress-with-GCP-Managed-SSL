# Kubernetes-ingress-with-GCP-Managed-SSL

Deploying Application with Domain Pointing on Ingress and Google Managed Certificate Attachment

Introduction:

This document outlines the steps to deploy an application on Kubernetes with a domain pointing to an Ingress resource, and attaching a Google Managed Certificate for HTTPS access.

Prerequisites:

- Access to Google Cloud Platform (GCP) console
- gcloud CLI installed and configured
- Kubernetes cluster set up on GCP
- Domain registered and managed in Cloud DNS

Step-by-Step Deployment

1. Reserve Static IP Address

First, reserve a static IP in GCP to use with the Ingress resource.
  
  gcloud compute addresses create nginxexample --global

Verify the creation and obtain details of the reserved static IP.
  
  gcloud compute addresses describe nginxexample --global

2. Create Kubernetes Manifest File
   
Create a Kubernetes manifest file (nginx-deployment.yaml) containing the deployment, service, Ingress, and ManagedCertificate sections. Replace placeholders with actual configurations and your reserved static IP.

3. Deployment and Access
   
Deploy the application using the created manifest file.
  
  kubectl apply -f nginx-deployment.yaml

For verfication access the application using the Kubernetes Service external IP, which should be your LoadBalancer IP.

4. Configure Ingress and Domain
   
Get the Ingress external IP and update Cloud DNS in the public zone to point your domain to this IP.
  
  kubectl get ingress -n flowise nginx-ingress

5. Verification and Troubleshooting

Check the deployed resources in Kubernetes and GCP for verification and troubleshooting.
kubectl get svc -n flowise nginx-svc
kubectl get ingress -n flowise nginx-ingress
kubectl get managedcertificates -n flowise managed-cert  --- > it should show ACTIVE

Also, verify resources in GCP console for more clarity.

Remember:
-  Ensure proper naming and labeling of resources.
-  Replace placeholders with actual values in the manifest file.
-  Verify DNS propagation after updating Cloud DNS settings.
-  Troubleshoot any issues using Kubernetes and GCP resources.
-  GCP Managed SSL Certificate will take 10 to 20 mints minimum for successfully provioning.
-  Once SSL Certificate will provision successfully. you can access your application through browser with HTTPS as well. Sometime it take few minuts for getting up..
