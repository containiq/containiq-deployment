# ContainIQ

### What it does 
Get notified in slack when things go wrong (or right) in your cluster and observe event trends over time in 
your containiq dashboard

![Alt text](logo.png "Title")

### How it Works
The containiq agents utilizes the kubernetes informer api to watch for events 
and notify you when things change. You can filter based on resource, namespace or event type. 

#### Using kubectl 
The `deployment.yaml` file contains all the necessary resources to run 
the containiq agent in your cluster. 

To get started update the `deployment.yaml` file's config map object with the resources and namespaces you would like to track. Next add your api keys to the 
secret object and choose which notification channels you would like enable. 

Finally run `kubectl apply -f deployment.yaml `
### integrating with slack 
Start by using the button below and writing down the token it provides. This token should then be substituted in the slack key field in the kubernetes secret object. <br> 

<a href="https://slack.com/oauth/v2/authorize?client_id=1494122840611.1544827505748&scope=chat:write&user_scope="><img alt="Add to Slack" height="40" width="139" src="https://platform.slack-edge.com/img/add_to_slack.png" srcSet="https://platform.slack-edge.com/img/add_to_slack.png 1x, https://platform.slack-edge.com/img/add_to_slack@2x.png 2x" /></a>

Next invite the containiq bot, by using the command `/invite @containiq` in your channel of choice 

### Using Helm 
`helm repo add containiq https://containiq.github.io/charts/`
`helm repo update`
#### Helm example install 
```
helm install containiq containiq/containiq --namespace=containiq \
 --set comm.Source.Slack.enabled=true \
 --set comm.Source.Slack.channel=testing \
 --set comm.Source.Slack.Key=<SLACK_TOKEN> \
 --set comm.Source.Containiq.Key=<CONTAINIQ_API_KEY> \
 --set configuration.monitoring.namespaces.watch="{default,namespace2}" 
 ```
 
for a full list of available configuration options please see values.yaml file in helm/containiq/


 
