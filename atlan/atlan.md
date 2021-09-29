# Solution Implementation
1. These are the steps to be performed in the atlan namespace.

# Steps
## Namespace creation
* kubectl create ns atlan

## Install nginx
1. Add the chart for nginx ingress controller.
    * helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
2. Update the helm repository.
    * helm repo update
3. Deploy the ingress-nginx chart in the atlan namespace.
    * helm install ingress-nginx ingress-nginx/ingress-nginx -n atlan