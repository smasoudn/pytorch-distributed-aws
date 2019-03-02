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
....
<a name="env"/>
## Seting up Environments
....
<a name="code"/>
## Distributed Coding
....

