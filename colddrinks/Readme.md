# Adding basic sample charts
helm repo add azure-samples https://azure-samples.github.io/helm-charts/

# colddrinks_corporation
helm install juice azure-samples/aks-helloworld `
    --namespace colddrinks `
    --set title="Time to drink juice          -colddrinks_corporation" `
    --set serviceName="juice"

helm install milkshake azure-samples/aks-helloworld `
    --namespace colddrinks `
    --set title="Time to drink milkshake          -colddrinks_corporation" `
    --set serviceName="milkshake"

USER="colddrinks"; PASSWORD="colddrinks"; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth
kubectl create secret generic basic-auth --from-file=auth -n colddrinks

kubectl get resourcequota resourcequota --namespace=colddrinks --output=yaml

PS C:\Users\bibhavj\k8s\atlan\colddrinks> kubectl.exe apply -f .\dummy_colddrinks_consumer.yaml -n colddrinks
Error from server (Forbidden): error when creating ".\\dummy_colddrinks_consumer.yaml": pods "dummycolddrinksconsumer" is forbidden: exceeded quota: resourcequota, requested: limits.cpu=800m,limits.memory=800Mi,requests.cpu=400m,requests.memory=600Mi, used: limits.cpu=0,limits.memory=0,requests.cpu=0,requests.memory=0, limited: limits.cpu=500m,limits.memory=512Mi,requests.cpu=250m,requests.memory=256Mi
