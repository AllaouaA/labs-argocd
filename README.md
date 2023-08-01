#### Hands-on-ArgoCD-AppSet

```bash
# create k8s cluster with docker-desktop or kind https://kind.sigs.k8s.io/docs/user/quick-start/

# make sure you are using the correct context
kubectl config get-contexts                          # display list of contexts
kubectl config current-context                       # display the current-context
kubectl config use-context docker-desktop           # set the default context

# install ArgoCD
kubectl create -f argocd-install/ns.yaml
kubectl create -n argocd -f argocd-install/install.yaml

# check argocd pods status
kubectl get po -n argocd -w

# access the argocd UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below pwd
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# install the application "myapp-argo-application"
kubectl apply -f demo/application.yaml
 
# Access the demo Application 
kubectl get svc -n demo 
kubectl port-forward svc/myapp-service 8085:8080 -n demo

# ApplicationSet controller is already installed
# install the demo applicationSet
kubectl apply -f appset/application.yaml




# TODO
# Add myapp-prod using values-prod

```
</br>

#### Links


* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)
