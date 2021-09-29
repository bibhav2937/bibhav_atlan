# Solution Implementation
1. These are the steps to be performed in the softdrinks namespace.

# Steps
## Namespace creation
    `kubectl create ns softdrinks`

## No resource quota set-up for softdrinks
As softdrinks customer uses dynamic-pricing-model. We dont need to create any resource quota for this namespace.

## Deploy services in the softdrinks namespace
1. Deploy pepsi service.
----
`
helm install pepsi azure-samples/aks-helloworld `
    --namespace softdrinks `
    --set title="Time to drink pepsi          -softdrinks_corporation" `
    --set serviceName="pepsi"
`

# softdrinks_corporation
helm install pepsi azure-samples/aks-helloworld `
    --namespace softdrinks `
    --set title="Time to drink pepsi          -softdrinks_corporation" `
    --set serviceName="pepsi"

## Create a named-auth file using openssl

    `USER="softdrinks"; PASSWORD="softdrinks"; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth`

## Create a basic-auth secret object
    ` kubectl create secret generic basic-auth --from-file=auth -n softdrinks`

## Deploy the ingress rules
1. Ingress rules are defined in the [newingress_softdrinks.yaml](newingress_softdrinks.yaml) file.
2. Deploy the ingress rules in the softdrinks namespace.

        ` kubectl apply -f newingress_softdrinks.yaml -n softdrinks`







