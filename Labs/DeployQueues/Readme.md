# Deploying Queues

 <img src="./Images/DeployQueues.png" width="500px"/> 
  
  The Microservice Cafe implentation follows a microservices architecture and utilizes Azure Service Bus Queues to exchange messages through out the different services.

## Core Technologies

* <a href="https://docs.microsoft.com/en-us/azure/service-bus-messaging">Azure Service Bus</a>
  
## Step-by-step 

* We will using the Azure CLI to create the required Azure resources. Using your favorite shell (PowerShell, Bash, ...etc), verify that the Azure CLI is installed by running 
  ```
  az version
  ```
* If the CLI is installed, we will need to login the CLI into your Azure subscription. Follow the prompts after running the `login` command
  ```
  az login
  ```
* Create the resource group that we will use to group all resources in this lab
  ```
  az group create -n microservicescafe -l eastus
  ```
* Create a Service Namespace
  ```
  az servicebus namespace create --resource-group microservicescafe --name microservicescafe \
      --location eastus --sku Standard
  ```
* Now that we have a namespace lets create the "Pending Orders" and "Completed Orders" queues
  ```
  az servicebus queue create --resource-group microservicescafe --namespace-name microservicescafe \
      --name pendingorders
  az servicebus queue create --resource-group microservicescafe --namespace-name microservicescafe \
      --name completedorders
  ``` 
* Lastly, we need to retrive a connection string for our newly created Azure Service Bus, we will need it later.
  ```
  az servicebus namespace authorization-rule keys list --resource-group microservicescafe \
      --namespace-name microservicescafe -n RootManageSharedAccessKey
  ```

## Next Steps

* <a href="/Labs/CashierService/Readme.md" class="myButton">Cashier Service and Azure App Services</a>
  