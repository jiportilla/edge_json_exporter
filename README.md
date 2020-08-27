# Edge JSON Exporter
Edge Node JSON Exporter

This is a simple example of using and creating a JSON Exporter service.

- [Preconditions for Using the JSON Exporter Service](#preconditions)
- [Using the JSON Exporter Service with Deployment Policy](PolicyRegister.md)
- [Creating Your Own Prometheus-operator monitoring solution](CreateService.md)
- Further Learning - to see more Horizon features demonstrated, continue on to the [cpu2evtstreams example](../../evtstreams/cpu2evtstreams).

## <a id=preconditions></a> Preconditions for Using the JSON Exporter Service

If you have not done so already, you must do these steps before proceeding with the JSON Exporter service:

1. Install the Horizon management infrastructure (exchange and agbot).

	*Also see [one-click Management Hub installation example](https://github.com/open-horizon/devops/blob/master/mgmt-hub/README.md)

2. Install the Horizon agent on your edge device and configure it to point to your Horizon exchange.

3. As part of the infrasctucture installation process for IBM Edge Computing Manager a file called `agent-install.cfg` was created that contains the values for `HZN_ORG_ID` and the exchange and css url values. Locate this file and set those environment variables in your shell now:

```bash
eval export $(cat agent-install.cfg)
```

 - **Note**: if for some reason you disconnected from ssh or your command line closes, run the above command again to set the required environment variables.

4. In addition to the file above, an API key associated with your Horizon instance would have been created, set the exchange user credentials, and verify them:

```bash
export HZN_EXCHANGE_USER_AUTH=iamapikey:<horizon-API-key>
hzn exchange user list
```

5. Choose an ID and token for your edge node, create it, and verify it:

```bash
export HZN_EXCHANGE_NODE_AUTH="<choose-any-node-id>:<choose-any-node-token>"
hzn exchange node create -n $HZN_EXCHANGE_NODE_AUTH
hzn exchange node confirm
```

6. If you have not done so already, unregister your node before moving on:
 ```bash
hzn unregister -f
```

## <a id=using-helloworld-pattern></a> Using the JSON Exporter Service with Deployment Pattern

1. Register your edge node with Horizon to use the helloworld pattern:

```bash
hzn register
```
 - **Note**: using the `-s` flag with the `hzn register` command will cause Horizon to wait until agreements are formed and the service is running on your edge node to exit, or alert you of any errors encountered during the registration process.

2. After the agreement is made, list the docker container edge service that has been started as a result:

``` bash
sudo docker ps
```

3. See the helloworld service output:

``` bash
curl localhost:7979/eventlog
```
 - **Note**: Press **Ctrl C** to stop the command output.

4. Unregister your edge node (which will also stop the myhelloworld service):

```bash
hzn unregister -f
```
