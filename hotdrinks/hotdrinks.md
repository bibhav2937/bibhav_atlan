# Solution Implementation
1. These are the steps to be performed in the hotdrinks namespace.

# Steps
## Namespace creation
    `kubectl create ns hotdrinks`

## Set resource quota
1. We need to set the resource quota for hotdrinks company because the hotdrinks consumer is using Fixed-resource-quota model.
2. Implement a ResourceQuota object in the colddrinks namespace using the [quota.yaml](quota.yaml) file.

    `kubectl apply -f quota.yaml -n hotdrinks`

## Deploy services in the hotdrinks namespace
1. Deploy tea service.
----
`
helm install tea azure-samples/aks-helloworld `
    --namespace hotdrinks `
    --set title="Time to drink tea          -hotdrinks_corporation" `
    --set serviceName="tea"
`

2. Deploy coffee service

`
helm install coffee azure-samples/aks-helloworld `
    --namespace hotdrinks `
    --set title="Time to drink coffee          -hotdrinks_corporation" `
    --set serviceName="coffee"

----

## Create a named-auth file using openssl

    `USER="hotdrinks"; PASSWORD="hotdrinks"; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth`

## Create a basic-auth secret object
    ` kubectl create secret generic basic-auth --from-file=auth -n hotdrinks`

## Deploy the ingress rules
1. Ingress rules are defined in the [newingress_hotdrinks.yaml](newingress_hotdrinks.yaml) file.
2. Deploy the ingress rules in the hotdrinks namespace.

        ` kubectl apply -f newingress_hotdrinks.yaml -n hotdrinks`

## Check the resourcequota.
1. Check the resourcequota due to the resource deployed in the hotdrinks namespace.

        `kubectl get resourcequota resourcequota --namespace=hotdrinks --output=yaml`
2. Observe the namespace has unused mem and cpu limits available in the hotdrinks namespace.
`
