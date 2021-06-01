# ContainIQ

![Alt text](logo.png "Title")


## How to install
### Install the metrics server
Check if it's already installed 

```kubectl get pods --all-namespaces | grep metrics-server```

If nothing is returned, install it with the command below 

```
git clone https://github.com/kubernetes-sigs/metrics-server.git
cd metrics-server
kubectl apply -f deploy/kubernetes/
```
#### Install the agent 

### Using kubectl 
Download the deployment file \
 `curl -L -o deployment.yaml https://raw.githubusercontent.com/containiq/containiq-deployment/master/deployment.yaml`

The `deployment.yaml` file contains all the necessary resources to run 
the containiq agent in your cluster. 

Add your api key to the secret object at the bottom of the `deployment.yaml` file.
  
Finally run `kubectl apply -f deployment.yaml `

### Using Helm 
`helm repo add containiq https://containiq.github.io/charts/`
`helm repo update`

#### Helm 2
```
helm install containiq containiq/containiq --namespace=containiq \
 --set comm.Key=<CONTAINIQ_API_KEY> \
 ```

#### Helm 3
 
 ```
helm install containiq containiq/containiq --namespace=containiq \
--create-namespace \
--set comm.Source.Key=<CONTAINIQ_API_KEY> \
```


## Setting up notifications

### Integrating with slack 
Click [here](https://app.containiq.com/profile/integration) to add your slack workspace and channel for notifications. 

###Creating Monitors
Click [here](https://app.containiq.com/profile/monitors) to create monitors for your kubernetes events and metrics 
 
