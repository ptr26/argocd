minikube delete --all 
minikube start -p argocd --kubernetes-version=latest

# install argo
kubectl create ns argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.5.8/manifests/install.yaml

# connect to the GUI
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
minikube service argocd-server --url -n argocd --profile argocd

# deploy app
