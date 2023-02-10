# Deploy a application to Kubernetes through ArgoCD and GitOps

Prerequisites
- Make sure you have a cluster ready on your terminal
- ArgoCD is installed on the cluster

You can install ArgoCD with the following commands

- This is optional, you can create a namespace "argocd" or go ahead with the "defautl" namespace<br>
`kubectl create namespace argocd`

- Run the install ArgoCD script <br>
`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`

- Install the CLI with brew, for using the argocd commands <br>
`brew install argocd`

- Enter the following command for getting the password <br>
`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`

- Forward the port to 8080, for accessing it on browser <br>
`kubectl port-forward svc/argocd-server -n argocd 8080:443`

- Now switch to another terminal, and make sure it keeps on running the forward command in the previous one

# Deployment

- Use the create command for creating the deployment <br>
`argocd app create zomato-clone --repo https://github.com/argoproj/argocd-example-apps.git --path dev --dest-server https://kubernetes.default.svc --dest-namespace default` 

zomato-clone-> Name of your application
--repo-> Repository URL of the application
--path-> The path where all the YAML files are located in the repository
--dest-server-> Destination cluster URL
--dest-namespace-> The namespace 

![image](https://user-images.githubusercontent.com/84350895/218014312-01eebe34-86d7-42fc-b671-a778af6080a7.png)


- Now use the sync command for deploying <br>
`argocd app sync zomato-clone`

![image](https://user-images.githubusercontent.com/84350895/218012484-a9d5db47-948f-410d-9dae-e85c5366cbc6.png)


- You can check the status by <br>
`argocd app get zomato-clone` 

![image](https://user-images.githubusercontent.com/84350895/218013110-83400e16-daa0-4516-90d6-d88b3906a070.png) <br>

![image](https://user-images.githubusercontent.com/84350895/218012814-b7d30a12-f7a1-4352-aec4-4e13e6d062ba.png)


- Let's check the services <br>
`kubectl get svc` 

![image](https://user-images.githubusercontent.com/84350895/218014513-74a7d6e9-aadc-4d24-bd2e-539874ad52cf.png)


- Port forwarding for accessing the application on port 9090 <br>
`kubectl port-forward svc/zomato-clone 9090:80` 

![image](https://user-images.githubusercontent.com/84350895/218014621-64fd82ef-da9a-437b-91d5-888eb9847502.png) <br>

Application Deployed through CLI 🎉, you can also do this through the UI 🚀








