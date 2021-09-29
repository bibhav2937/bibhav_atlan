# Solution Implementation
1. These are the steps to be performed in the colddrinks namespace.

# Steps
## Namespace creation
    `kubectl create ns colddrinks`

## Set resource quota
1. We need to set the resource quota for colddrinks company because the colddrinks consumer is using Fixed-resource-quota model.
2. Implement a ResourceQuota object in the colddrinks namespace using the [quota.yaml](quota.yaml) file.

    `kubectl apply -f quota.yaml -n colddrinks`

## Deploy services in the colddrinks namespace
1. Deploy juice service.
----
`
helm install juice azure-samples/aks-helloworld `
    --namespace colddrinks `
    --set title="Time to drink juice          -colddrinks_corporation" `
    --set serviceName="juice"
`

2. Deploy milkshake service

`
helm install milkshake azure-samples/aks-helloworld `
    --namespace colddrinks `
    --set title="Time to drink milkshake          -colddrinks_corporation" `
    --set serviceName="milkshake"

----

## Create a named-auth file using openssl

    `USER="colddrinks"; PASSWORD="colddrinks"; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth`

## Create a basic-auth secret object
    ` kubectl create secret generic basic-auth --from-file=auth -n colddrinks`

## Deploy the ingress rules
1. Ingress rules are defined in the [newingress_colddrinks.yaml](newingress_colddrinks.yaml) file.
2. Deploy the ingress rules in the colddrinks namespace.

        ` kubectl apply -f newingress_colddrinks.yaml -n colddrinks`

## Check the resourcequota.
1. Check the resourcequota due to the resource deployed in the colddrinks namespace.

        `kubectl get resourcequota resourcequota --namespace=colddrinks --output=yaml`
2. Observe the namespace has unused mem and cpu limits available in the colddrinks namespace.

## Deploy resources to exceed the resourcequota limits
1. Try to deploy a pod resource that has resource requirements within the namespace limits.
    ` kubectl apply -f allowed_pod.yaml -n colddrinks`
2. Deploy another pod so that resource requirements exceed the namespace limits.
    ` kubectl apply -f failed_pod.yaml -n colddrinks`
3. Verify the second pod deployment failed with following error.
`
PS C:\Users\bibhavj\k8s\bibhav_atlan\colddrinks> kubectl.exe apply -f .\failed_pod.yaml -n colddrinks
Error from server (Forbidden): error when creating ".\\failed_pod.yaml": pods "failedpod" is forbidden: exceeded quota: resourcequota, requested: requests.cpu=150m,requests.memory=161061273600m, used: requests.cpu=150m,requests.memory=161061273600m, limited: requests.cpu=250m,requests.memory=256Mi
`
