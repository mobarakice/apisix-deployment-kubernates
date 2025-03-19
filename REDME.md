# DEPLOY APISIX AND APISIX-DASHBOARD with Kubernates minikube

## Prerequisite

- Install kubectl
- Install minikube

# Deployment steps

- Step1: Start the minikube

    `minikube start`
- Step2: start the minikube dashboard

    `minikube dashboard`
- Step3: Enable metrics-server

    `minikube addons enable metrics-server`
- Step4: Build the apisix and apisix-dashboard images and push into minikube docker deamon
  
  - build apisix image
  
    `docker build -t apisix:3.11.0`
  - load this image into minikube
    
    `minikube image load apisix:3.11.0`

  - build apisix-dashboard image

  `docker build -t apisix-dashboard:3.0.2`
  - load this image into minikube

    `minikube image load apisix-dashboard:3.0.2`
- Step5: Deploy the etcd, apisix, and apisix-dashboard
   
    ```
    kubectl apply -f etcd.yaml
    kubectl apply -f apisix.yaml
    kubectl apply -f dashboard.yaml
  ```

- Step6: check deployment list, pods list and logs

    - check deployment list
        
      `kubectl get deployments`
    - check pods
    
       `kubectl get pods`
    - check logs of a pod
         
       `kubectl logs <pod_name>`
    - 
       
- Step7: Forward apisix and apisix-dashboard port
   
    - apisix port forwarding
        `kubectl port-forward svc/apisix 9080:9080`
    - apisix-dashboard port forwarding
      `kubectl port-forward svc/apisix-dashboard 9000:9000`
- Finally, access apisix and apisix-dashboard with following urls
   - [Dashboard]("http://localhost:9000")
   - [APISIX]("http://localhost:9080")