---
id: setup-private-net
title: Setup Private Network
sidebar_label: Setup Private Network
description: >-
  On this page, you will learn how to set up and bootstrap a private MakeOS
  network on your local machine. We will be creating a four (4) node local
  network where all the nodes are validators.
---

# Set Up a Private Network

## Step 1: Create Keys

Each node must be initialized with a unique validator key that will be used to identify the node and sign operations. We need to create a validator key for each of the nodes.

### Node 1

{% tabs %}
{% tab title="Bash" %}
```bash
kit key gen
```
{% endtab %}

{% tab title="Output" %}
```
Private Key: wgDGBTjRMawhiM4RfBrTJXCt...pTkcndMWmUSZi67zATqZ4
Public Key:  489XdyeZjDqx4GQiegutACHpeJb89ZBL5K3XEmfZTJtr1CcPJy1
```
{% endtab %}
{% endtabs %}

### Node 2

{% tabs %}
{% tab title="Bash" %}
```bash
kit key gen
```
{% endtab %}

{% tab title="Output" %}
```
Private Key: wcDVvz3UwHzPc2RxjtZVso1G...yd3Hc9GE7acZT74ARYpUXJ
Public Key:  49Ejroft49qZjvf8aAbUfhJEXtAy4L9W5rotS1z8v494Ebjxb
```
{% endtab %}
{% endtabs %}

### Node 3

{% tabs %}
{% tab title="Bash" %}
```bash
kit key gen
```
{% endtab %}

{% tab title="Output" %}
```
Private Key: wLPUBRgJ1kQ73AVaqfZ9vpfbNuu...68RYw8kG7gJ8qwmZC27EuQ
Public Key:  47p1YrT93a5m33SHsqH3CU1n3vYW7CR2bybjd4SNVicYLQ1CcSC
```
{% endtab %}
{% endtabs %}

### Node 4

{% tabs %}
{% tab title="Bash" %}
```bash
kit key gen
```
{% endtab %}

{% tab title="Output" %}
```
Private Key: wKQDFQiw4JYTUdeER2jx9ysP8rh...G4WUdZRc7vjYpmM16bDcy
Public Key:  48gR6x2Vym5M2dUfS3TpwqUYuhLqE91gxEmYRXaK7UFqVY6De5Z
```
{% endtab %}
{% endtabs %}

We use the command `kit key gen`  to generate an Ed25519 keypair. MakeOS uses Ed25519 public key signature system for signing and verifying operations.

{% hint style="info" %}
Output from the `kit key gen` command will not match the output in the example above. This is normal.
{% endhint %}

## Step 2: Initialize Nodes

Next, we must initialize the nodes individually so that they have their own data directory, configurations and are isolated from each other on the same machine. 

The `kit init` command tags the following flags when initializing a new node:

* `-v`: The list of public keys of the nodes that will become the initial network validators.
* `-k`: The validator private key of the node.
* `-t`: The network's official launch Unix timestamp. 

### Node 1

```bash
kit init --home.id n1 \
   -v=489XdyeZjDqx4GQiegutACHpeJb89ZBL5K3XEmfZTJtr1CcPJy1,\
      49Ejroft49qZjvf8aAbUfhJEXtAy4L9W5rotS1z8v494Ebjxb, \
      47p1YrT93a5m33SHsqH3CU1n3vYW7CR2bybjd4SNVicYLQ1CcSC \
      48gR6x2Vym5M2dUfS3TpwqUYuhLqE91gxEmYRXaK7UFqVY6De5Z \
   -k=wgDGBTjRMawhiM4RfBrTJXCt...pTkcndMWmUSZi67zATqZ4 \
   -t=1595700581
```

### Node 2

```bash
kit init --home.id n2 \
   -v=489XdyeZjDqx4GQiegutACHpeJb89ZBL5K3XEmfZTJtr1CcPJy1,\
      49Ejroft49qZjvf8aAbUfhJEXtAy4L9W5rotS1z8v494Ebjxb, \
      47p1YrT93a5m33SHsqH3CU1n3vYW7CR2bybjd4SNVicYLQ1CcSC \
      48gR6x2Vym5M2dUfS3TpwqUYuhLqE91gxEmYRXaK7UFqVY6De5Z \
   -k=wcDVvz3UwHzPc2RxjtZVso1G...yd3Hc9GE7acZT74ARYpUXJ \
   -t=1595700581
```

### Node 3

```bash
kit init --home.id n3 \
   -v=489XdyeZjDqx4GQiegutACHpeJb89ZBL5K3XEmfZTJtr1CcPJy1,\
      49Ejroft49qZjvf8aAbUfhJEXtAy4L9W5rotS1z8v494Ebjxb, \
      47p1YrT93a5m33SHsqH3CU1n3vYW7CR2bybjd4SNVicYLQ1CcSC \
      48gR6x2Vym5M2dUfS3TpwqUYuhLqE91gxEmYRXaK7UFqVY6De5Z \
   -k=wLPUBRgJ1kQ73AVaqfZ9vpfbNuu...68RYw8kG7gJ8qwmZC27EuQ \
   -t=1595700581
```

### Node 4

```bash
kit init --home.id n4 \
   -v=489XdyeZjDqx4GQiegutACHpeJb89ZBL5K3XEmfZTJtr1CcPJy1,\
      49Ejroft49qZjvf8aAbUfhJEXtAy4L9W5rotS1z8v494Ebjxb, \
      47p1YrT93a5m33SHsqH3CU1n3vYW7CR2bybjd4SNVicYLQ1CcSC \
      48gR6x2Vym5M2dUfS3TpwqUYuhLqE91gxEmYRXaK7UFqVY6De5Z \
   -k=wKQDFQiw4JYTUdeER2jx9ysP8rh...G4WUdZRc7vjYpmM16bDcy \
   -t=1595700581
```

These commands will create 4 data directories, one for each node. You can find them in `$HOME/.kit_n{1-4}`.

## Bootstrap The Network

If you successfully initialized the nodes in the last section, you are now ready to run them and create your very own local network.

### **Run the first node: n1**

Start the first node with RPC service turned on so we can attach to it from another terminal.

{% tabs %}
{% tab title="Bash" %}
```bash
kit start --home.id=n1 --rpc.on
```
{% endtab %}

{% tab title="Output" %}
```
INFO[0000] [node]: Starting node...                      DevMode=true NodeID=ac2ce8d01b1f26663ed30776503339bd3f6c684d
INFO[0000] [node]: App database has been loaded          AppDBDir=/Users/name/.lobe_n1/1/data/appdata.db
INFO[0000] [remote-server]: Server has started           Address="127.0.0.1:9004"
INFO[0000] [node]: Now listening for connections         Address="ac2ce8d01b1f26663ed30776503339bd3f6c684d@127.0.0.1:9000"
```
{% endtab %}
{% endtabs %}

 On a successful startup, the node will output details about its start and operation. Take note of the connection address, we will use it to get the other nodes to join the network started by `n1`. 

#### Connect the other nodes

Open three \(3\) new terminals and run each command below on each of them. The commands starts `n2`, `n3` and `n4`, connecting them to `n1`. 

```text
kit start --home.id=n2 \
   --node.address=127.0.0.1:8000 \
   --rpc.tmaddress=127.0.0.1:8001 \
   --node.addpeer=ac2ce8d01b1f26ac2ce8d01b1f26663ed30776503339bd3f6c684d@127.0.0.1:9000
```

```bash
kit start --home.id=n3  \
    --node.address=127.0.0.1:7000  \
    --rpc.tmaddress=127.0.0.1:7001  
    --node.addpeer=ac2ce8d01b1f26ac2ce8d01b1f26663ed30776503339bd3f6c684d@127.0.0.1:9000
```

```text
```shell script
kit start --home.id=n4 \
   --node.address=127.0.0.1:6000 \
   --rpc.tmaddress=127.0.0.1:6001 \
   --node.addpeer=ac2ce8d01b1f26ac2ce8d01b1f26663ed30776503339bd3f6c684d@127.0.0.1:9000
```

On success, all nodes will be connected and block creation will begin. Since all nodes are validators, they will take turns proposing new blocks.

Since Tendermint can tolerate `1/3` of nodes failing; 1 validator can go offline or become unresponsive and the network will still continue to create new blocks and process transactions.

## Transfer Coins

Once you have a running node, you test the network by transferring the native coins from one account to another by using the [user](../console/user.md) API available in the console mode.

#### Attach to the running node \(n1\)

To access the console API, we must attach to a running node. If you followed previous private network setup walkthrough, you can connect to `n1` and start a console session with the following command

```bash
kit attach
```

#### Create a recipient address

We need to create the address that will receive the coins we will send. You can use `kit key gen` to generate an address but since we are already in the console, you can use `util.genKey` method.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
> util.genKey()
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
   "address": "os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd",
   "privateKey": "wqEoX3B8o1M8SkU...eantBMK3XDZSvc8V8gSYu",
   "publicKey": "48u65FLpzAGNCepxPUAHaGQLwpbZyD7pRZ6AWhw6yaYHQ9p9HN5"
}
```
{% endtab %}
{% endtabs %}

#### Send Coins From Dev Account

When Kit is initialized in development mode, it creates a user account with an initial supply of `2,000,000` coins for development or testing purpose. The account's address and private key can be accessed via `dev.accountAddress` and `dev.accountKey`respectively.  

We are going to transfer 1,000 coins from the dev account to the beneficiary address we created earlier. We will use the `user.send` method. 

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.send({ 
   to: "os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd",  
   value:"1000", 
   fee: "1" 
}, dev.accountKey)
```
{% endtab %}

{% tab title="Output" %}
```javascript
{ "hash": "0xe971c8665e3430dd5a1d...b5dcc765b631dea133" }
```
{% endtab %}
{% endtabs %}

The hash of the transaction is returned when the transaction has been successfully validated and added into the Mempool. The transaction becomes processed when it is added to the next block by a block validator.

**Check the balance**

Let’s check the balance of the sender and the beneficiary. We use `user.getBalance` to check the account balance of an address. 

{% tabs %}
{% tab title="Bash" %}
```bash
user.getBalance(dev.accountAddress)
```
{% endtab %}

{% tab title="Output" %}
```javascript
"1999000"
```
{% endtab %}
{% endtabs %}

