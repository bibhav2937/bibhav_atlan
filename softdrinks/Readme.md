# softdrinks_corporation

## Steps
1. Create namespa

# softdrinks_corporation
helm install pepsi azure-samples/aks-helloworld `
    --namespace softdrinks `
    --set title="Time to drink pepsi          -softdrinks_corporation" `
    --set serviceName="pepsi"


USER="softdrinks"; PASSWORD="softdrinks"; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth
kubectl create secret generic basic-auth --from-file=auth -n softdrinks

kubectl get resourcequota resourcequota --namespace=hotdrinks --output=yaml







