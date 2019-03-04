# [WIP] pytorch-distributed-aws
This tutorial walks you through setting up a distributed training setting on AWS using PyTorch 1.0.

The goal is to run distributed training across **multi-nodes** and **multi-GPUs**.

### Table of Contents  
[Setting up Amazon AWS](#aws_setup)  
[Configuring Security Group](#security)  
[Setting up Environments](#env)
[Distributed Coding](#code)
<a name="aws_setup"/>


## Setting up Amazon AWS
Here, we are going to launch *two* *multi-GPU* instances in AWS. If you do not have AWS account, create one [here](https://aws.amazon.com/). Create an instance by following the steps below:

**1.** Search for EC2 (Elastic Compute Cloud) service and click on *Launch Instance*.

**2. Choose AMI:**  As this example uses XXXX dataset to train a deep network and needs GPU, select *Deep Learning AMI (Amazon Linux)* AMI (Amazon Machine Image). You may search for *deep learning* in the search bar to find your AMI faster.

**3. Choose Instance Type:** Select an instance type. As we need GPU, we select *p2.8xlarge* instance type which has 8 GPUs.

**4. Configure Instanec:** To create two nodes,  set *Number of instances* to 2. No need to change other configs at this time.

**5. Add Storage:** This instance is comming with 75 GB space which is enough for this example. No need to change anything here.

**6. Add Tags:** No need to add any tag for this example.

**7. Configure Security Group:** By default two nodes in the same security group cannot communicate in a distributted training setting. To make the communication possible between nodes, create a *new security group* and remember the name you choose for this security group (e.g. launch-wizard-4). Remaining security settings will be done later.

**8. Review Instance Launch:** Review your instance configuration and launch it. When the initialization is complete, you see *2/2 checks ...* under the *Status Checks* tab in EC2 Dashboard - Instances.
.
.
<a name="security"/>
## Configuring Security Group
After launching the instances, from the EC2 dashboard, select *Network & Security > Security Group*. Select the security group name you chose in step 7 above, right click on it, and choose *Edit  inbound rules*. Remove all rules and add a new one with the type of *All traffic*. Right click on the  same security group name and repeat the above orocedure for the outbound rules. This way, you allow all inbound and outbound traffic between all nodes.
.
.
<a name="env"/>
## Seting up Environments
In EC2 dashboard and *Instances > Instances* tap, select each instance and remember its public and private IPv4. Public IPs are the addresses we use for SSH while the private ones will be used for inter-node communications.
We refer to IP addresses of each node as *node0_publicIP, node0_privateIP, node1_publicIP, node1_privateIP*.

We need to setup each node separately. Connect to each node using:
```
$ ssh -i "<PRIVATE KEY *.pem>" ec2-user@<INSTACE PUBLIC DNS>
```
If your instance does not have PyTorch, you may use conda to create a virtual environment and install PyTorch as below:
```
$ conda create -n pytorch_env python=3.6 numpy
$ source activate pytorch_env
$ pip install torch_nightly -f https://download.pytorch.org/whl/nightly/cu90/torch_nightly.html
```
We also need to install torchvision to use its models and  datasets:
```
$ cd
$ git clone https://github.com/pytorch/vision.git
$ cd vision
$ python setup.py install
```
The very important step is to set the network interface name for the NCCL socket. To get the network interface name use `ifconfig` command and look for a name corresponds to the node's *privateIP* (e.g. ens3). Then  set the environment variable as:
```
$ export NCCL_SOCKET_IFNAME=ens3
```
.
<a name="code"/>
## Distributed Coding
Some of important imports for distributed training are:
```
import torch.nn.parallel
import torch.distributed as dist
import torch.utils.data.distributed
from torch.multiprocessing import Pool, Process
....

