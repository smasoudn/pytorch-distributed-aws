# pytorch-distributed-aws
This tutorial walks you through setting up a distributed training setting on AWS using PyTorch 1.0.

The goal is to run distributed training across **multi-nodes** and **multi-GPUs**.

### Table of Contents  
[Setting up Amazon AWS](#aws_setup)  
[Configuring Security Group](#security)  
[Setting up Environments](#env)
[Distributed Coding](#code)
<a name="aws_setup"/>
## Setting up Amazon AWS
Here, we are going to launch **two** **multi-GPU** instances in AWS. If you do not have AWS account, create one [here](https://aws.amazon.com/). Create an instance by following the steps below:
**Step 1:** Search for EC2 (Elastic Compute Cloud) service and click on **Launch Instance**.

**Step 2 (Choose AMI):**  As this example uses XXXX dataset to train a deep network and needs GPU, select **Deep Learning AMI (Amazon Linux)** AMI (Amazon Machine Image). You may search for *deep learning* in the search bar to find your AMI faster.

**Step 3 (Choose Instance Type):** Select an instance type. As we need GPU, we select **p2.8xlarge** instance type which has 8 GPUs.

**Step 4 (Configure Instanec):** To create two nodes,  set *Number of instances* to 2. No need to change other configs at this time.

**Step 5 (Add Storage):** This instance is comming with 75 GB space which is enough for this example. No need to change anything here.

**Step 6 (Add Tags):** No need to add any tag for this example.

**Step 7 (Review Instance Launch):** Review your instance configuration and launch it. When the initialization is complete, you see *2/2 xxxx* under the *Instance State* tab in EC2 Dashboard - Instances.
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

