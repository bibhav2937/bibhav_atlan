# Adding basic sample charts
helm repo add azure-samples https://azure-samples.github.io/helm-charts/

# colddrinks_corporation
helm install tea azure-samples/aks-helloworld `
    --namespace hotdrinks `
    --set title="Time to drink tea          -hotdrinks_corporation" `
    --set serviceName="tea"

helm install milkshake azure-samples/aks-helloworld `
    --namespace hotdrinks `
    --set title="Time to drink coffee          -hotdrinks_corporation" `
    --set serviceName="coffee"

USER="colddrinks"; PASSWORD="colddrinks"; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth
kubectl create secret generic basic-auth --from-file=auth -n hotdrinks

kubectl get resourcequota resourcequota --namespace=hotdrinks --output=yaml

PS C:\Users\bibhavj\k8s\atlan\colddrinks> kubectl.exe apply -f .\dummy_colddrinks_consumer.yaml -n colddrinks
Error from server (Forbidden): error when creating ".\\dummy_colddrinks_consumer.yaml": pods "dummycolddrinksconsumer" is forbidden: exceeded quota: resourcequota, requested: limits.cpu=800m,limits.memory=800Mi,requests.cpu=400m,requests.memory=600Mi, used: limits.cpu=0,limits.memory=0,requests.cpu=0,requests.memory=0, limited: limits.cpu=500m,limits.memory=512Mi,requests.cpu=250m,requests.memory=256Mi
