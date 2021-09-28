# Atlan Hiring Challenge

## Problem Statement
link : https://www.notion.so/Hiring-Task-Senior-Cloud-Engineer-b67d07ffec45444f9ea96d64f0f2b885
To evaluate the Multi-tenancy approach and provide a detailed report with a working model for the multi-tenancy approach in Kubernetes. 

# Solution
The solution provides a working business model for multi-tenancy approach in Kubernetes. The solution is designed for a company named 'Atlan' that provides SaaS-offering hosting solution to the customers. For this demo, we will be treating 'Atlan' as the service provider company. 
Major components of the given business model is as given below.

! Company | Business Role | Namespace in cluster | Service offered/consumed | 
|---------------------------------------------------------------------------|
| Atlan | Service Provider | atlan | Offers a hosting platform for consumers |
| hotdrinks_corporation | consumer using Fixed-resource-quota model | hotdrinks | Service Name: tea, coffee |
| colddrinks_corporation | consumer using Fixed-resource-quota model | colddrinks | Service Name: juice, milkshake |
| softdrinks_corporation | consumer using Dynamic-pricing model | softdrinks | Service Name: pepsi |

## Business model
### Fixed-resource-quota model
1. Customers make a agreement with 'atlan' and fix the resource-quota limits (CPUs, Memory) for their usage. Atlan will charge the customers based on the fixed resourcequota.
2. Customers can request to bring-up any number of services till the total required resource consumption of the services is less than the limits of the agreement.
3. Atlan will guarantee that SLA is always met for the customer. Thus, system monitoring responsibility is with atlan.
4. Each customer will be given one namespace in the Atlan hosted kubernetes cluster.


### Dynamic-pricing model
1. Custumers dont make any hard-limit agreements with Atlan. Atan will charge the customers dynamically based on the pricing-slab for total resources used by the services deployed for the customers.
2. Customers can request to bring up any number of services till the pricing suits their budget.
3. Atlan will guarantee that SLA is always met for the customer. Thus, system monitoring responsibility is with atlan.
4. Each customer will be given one namespace in the Atlan hosted kubernetes cluster.

* Note: A customer needing multiple environments will be given a separate namespace for each environment in the atlan k8s cluster and will be charged separately for each namespace.