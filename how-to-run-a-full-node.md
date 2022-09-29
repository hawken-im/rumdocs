# How to run a full node?

{% hint style="info" %}
This tutorial is intended to guide users running full nodes on a Linux server using Quorum.&#x20;
{% endhint %}

{% hint style="info" %}
If your network provider properly provides upload bandwidth, or if you can configure NAT by yourself, you can run the full node client, Rum APP, locally, which is the same as what this tutorial is trying to achieve.
{% endhint %}



> Remote Environment：Unbuntu 20.04 + Quorum
>
> Local Environment：Windows 10 + Rum App V3.3.18

#### 0. What Is Full Node?

A full node is a concept that differs from a light node.&#x20;

In order to lower the user access barrier, the Rum team developed light nodes, through which users can join SeedNets and also browse and publish content. But with a light node, users cannot contribute to the Rum network, such as generating blocks and creating SeedNets.&#x20;

Full node users can use Rum's content management and publishing functions at the application level, and can also contribute to Rum Network.

#### 1. Why We Want to Run a Full Node?

The content of the Rum Network is aggregated and presented in different DApps by Groups (known as SeedNet at the application level). Groups are formed by different nodes that are linked together through a communication layer called Gossip Network. It can be seen that nodes are the base unit of the Rum System, and the nodes work together to serve the application level. As shown in the following figure:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>Rum System network structure diagram</p></figcaption></figure>

The founder of a full node has the following benefits and privileges:

1. Nodes that contribute network resources are subsidized by the economic system (economic system under construction).
2. A SeedNet created by a full node makes that node has administrator authority for that SeedNet.

#### Prerequisites

* Clone Quorum to the server

```
git clone git@github.com:rumsystem/quorum.git
```

{% hint style="info" %}
Repository: [https://github.com/rumsystem/quorum](https://github.com/rumsystem/quorum)
{% endhint %}

* Install the Golang

Follow the official Go language documentation: [https://go.dev/doc/install](https://go.dev/doc/install)

* Build Quorum through binary

Execute the command:

`make linux` or `make buildall`

The binaries are in the `dist` dir.

You can also Build Docker image files:

&#x20;`sudo docker build -t quorum`

#### Step 1 - Run Quorum Service

In this step, we will run the Quorum service on the server.

Execute the following command in the root directory where your `quorum` binaries are located:

{% code overflow="wrap" %}
```shell
./quorum fullnode --listen /ip4/0.0.0.0/tcp/{portNumber} --listen /ip4/0.0.0.0/tcp/{websocketPortNumber}/ws --apiport {apiPortNumber} --peer /ip4/94.23.17.189/tcp/10666/p2p/16Uiu2HAmGTcDnhj3KVQUwVx8SGLyKBXQwfAxNayJdEwfsnUYKK4u --configdir peerConfig --datadir peerData --keystoredir keystore --debug=false
```
{% endcode %}

Replace:`{portNumber}，{websocketPortNumber}，{apiPortNumber},` to port numbers vacancies.

If the server has a firewall, remember to allow the above ports open to the public traffic.

The first time you run `quorum`, you will be asked to generate a password, so keep it safe. You will need it when you run it again.

#### Step 2 - Acquire jwt token

In this step, we acquire the parameters that will be used to run the Rum App.

If you ran `quorum` in the `tmux` or `systemd`, system service, in the previous step, you can go directly to the root directory of `quorum` and continue executing commands to acquire the jwt token. Otherwise, you may need to stop the running quorum service.

Execute the following command in the root directory where your `quorum` binaries are located:

{% code overflow="wrap" %}
```shell
./quorum jwt create --configdir {quorumdir}/peerConfig chain --name node-all-groups
```
{% endcode %}

Replace `{quorumdir}` to dir of `quorum` .

After successfully executing the command, copy the text after `token:` and save it to your local computer. We will use it in the next step.

#### Step 3 - Connect Rum App to Quorum Service

In this step, we will connect to the remote Quorum service through the local Rum App to manage the running node.

First, [download the Rum App](applications.md#rum-app) and install it on your local computer.

Launch the Rum App and select "External Node" on the startup screen.

<img src=".gitbook/assets/Screen Shot 2022-09-29 at 23.08.23.png" alt="" data-size="original">

After selecting a local folder for storing local data, the next step is to fill in the required parameters:

![](<.gitbook/assets/Screen Shot 2022-09-29 at 23.07.38.png>)

Fill in the first blank with `http://{server IP address}:{apiPortNumber}`

Fill in the second blank with `jwt token` acquired in the previous step.

Click the "OK" button and wait for a while till successfully connect to the full node remotely via the local Rum App.

#### Conclusion

If any problems, try:

1. Use `./quorum -help` to check your command line.
2. Note if the firewall allows each port.
3. If you fail in trying repeatedly, please toggle on the DevTools of the Rum App to analyze the problem.

[Was this document helpful? Feel free to submit any issue or pull request to GitHub, thank you for your help.](https://github.com/hawken-im/rum-docs/blob/main/zen-yang-yun-hang-yi-ge-quan-jie-dian.md)
