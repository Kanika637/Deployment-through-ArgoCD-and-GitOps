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
`argocd app create zomato-clone --repo https://github.com/Kanika637/Deployment-through-ArgoCD-and-GitOps.git --path dev --dest-server https://kubernetes.default.svc --dest-namespace default` 

- zomato-clone-> Name of your application <br>
- --repo-> Repository URL of the application <br>
- --path-> The path where all the YAML files are located in the repository <br>
- --dest-server-> Destination cluster URL <br>
- --dest-namespace-> The namespace <br>

![image](https://user-images.githubusercontent.com/84350895/218014312-01eebe34-86d7-42fc-b671-a778af6080a7.png)


- Now use the sync command for deploying <br>
`argocd app sync zomato-clone`

![6](https://user-images.githubusercontent.com/84350895/218020315-f4c9c2c9-7b99-4aed-aa58-c9c966febe92.png)


- You can check the status by <br>
`argocd app get zomato-clone` 

![image](https://user-images.githubusercontent.com/84350895/218013110-83400e16-daa0-4516-90d6-d88b3906a070.png) <br>

![8](https://user-images.githubusercontent.com/84350895/218019906-4cfaec28-59c7-457a-aeec-11b5efb9679b.png)


- Let's check the services <br>
`kubectl get svc` 

![image](https://user-images.githubusercontent.com/84350895/218014513-74a7d6e9-aadc-4d24-bd2e-539874ad52cf.png)


- Port forwarding for accessing the application on port 9090 <br>
`kubectl port-forward svc/zomato-clone 9090:80` 

![1](https://user-images.githubusercontent.com/84350895/218020127-d78dff37-b3f2-4648-b4f7-7d6f13b6e43d.png)
 <br>

Application Deployed through CLI 🎉, you can also do this through the UI 🚀








