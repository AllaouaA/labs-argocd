#### Commands
# create k8s cluster with Kind
kind create cluster --name argo-demo

# install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f argocd-install/install.yaml

# check pods status
kubectl get po -n argocd -w

# access ArgoCD UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below token:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# Install our app myapp-argo-application
kubectl apply -f dev/application.yaml
 
# Acess to 'myapp' Application 
kubectl get svc -n myapp 

# install our application Set
kubectl apply -f app-set/application.yaml

# Test a port forward 
kubectl port-forward svc/myapp-1 8085:8080 -n myapp1


# TODO
 Deploy myapp-3 using a values-prod.yaml

```
</br>

#### Links


* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)
