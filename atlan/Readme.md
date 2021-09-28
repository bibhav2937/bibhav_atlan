# Install nginx
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx -n atlan

# Adding basic sample charts
helm repo add azure-samples https://azure-samples.github.io/helm-charts/

# Hotdrinks prod
helm install hotdrinks azure-samples/aks-helloworld `
    --namespace hotdrinks `
    --set title="Let's have HOTDRINKS          -hotdrinks_corporation" `
    --set serviceName="hotdrinks"

helm install toohothotdrinks azure-samples/aks-helloworld `
    --namespace hotdrinks `
    --set title="OMG!! Too hot HOTDRINKS.          -hotdrinks_corporation" `
    --set serviceName="toohothotdrinks"

kubectl create secret generic basic-auth --from-file=auth -n hotdrinks

