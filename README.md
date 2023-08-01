#### Commands

```bash
# create k8s cluster with docker-desktop

# check contexts
kubectl config get-contexts                          # display list of contexts
kubectl config current-context                       # display the current-context
kubectl config use-context docker-desktop           # set the default context to docker-desktop

# install ArgoCD => WD: argocd.labs
kubectl create -f argocd-install/ns.yaml
kubectl create -n argocd -f argocd-install/install.yaml

# check pods status
kubectl get po -n argocd -w

# access ArgoCD UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below pwd
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# you can change and delete init password
# Generating a bcrypt hash for the password: https://www.browserling.com/tools/bcrypt (test)
# bcrypt(password)=$2a$10$PwPtsXd6Cl9MSdQ2KiIG.upmIT2ObMTmZsI8/gW33PJZz553IkPTW
# enocde bcrypt(password)=JDJhJDEwJFB3UHRzWGQ2Q2w5TVNkUTJLaUlHLnVwbUlUMk9iTVRtWnNJOC9nVzMzUEpaejU1M0lrUFRX
kubectl -n argocd patch secret argocd-secret  -p '{"data": {"admin.password": "JDJhJDEwJFB3UHRzWGQ2Q2w5TVNkUTJLaUlHLnVwbUlUMk9iTVRtWnNJOC9nVzMzUEpaejU1M0lrUFRX", "admin.passwordMtime": ""}}'
kubectl -n argocd scale deployment argocd-server --replicas=0
kubectl -n argocd scale deployment argocd-server --replicas=1

# Install our app myapp-argo-application
kubectl apply -f demo/application.yaml
 
# Acess to demo Application 
kubectl get svc -n demo 
kubectl port-forward svc/myapp-service 8085:8080 -n demo

# ApplicationSet controller is already installed
# deploy ApplicationSet
kubectl apply -f appset/application.yaml




# TODO
# Add myapp-prod using values-prod

```
</br>

#### Links


* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)
