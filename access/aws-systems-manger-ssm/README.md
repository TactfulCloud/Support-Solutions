---
description: Describes the use and implementation of AWS SSM for secure access.
---

# AWS Systems Manger \(SSM\)

## Systems Manager Purpose

The AWS Systems Manager service provides many different features for providing visibility, control, compliance, and monitoring of your AWS EC2 Compute Instances.

AWS SSM is a key component of how Tactful Cloud securely accesses, modifies, and reports on resources in your environment. In order for Tactful Cloud to safely and securely manage your resources, we highly encourage the use and implementation of the AWS Systems Manager Agent. 

{% hint style="warning" %}
AWS SSM is not required for Tactful Cloud access; however, its implementation is highly encouraged.
{% endhint %}

By installing the AWS SSM Agent on your EC2 instance, you provide both your team and Tactful Cloud secure access to your resources and vital information without introducing the requirement to share SSH Key, or usernames and passwords. An added

## Compatibility

Depending on how you provisioned your instances or the image you used during deployment, the SSM Agent may already be present on your operating system. In some cases, the Agent may need to be installed or it is not compatible with your operating system.

## Service Details

The Systems Manager service and Agent are provided at no additional cost. There are some aspects of the service that may cost or leverage other AWS services that have some cost tied to them.

Listed here are links to resources to learn more about the AWS Systems Manager Service and Agent.

* Brochure Page - [https://aws.amazon.com/systems-manager/](https://aws.amazon.com/systems-manager/)
* Pricing - [https://aws.amazon.com/systems-manager/pricing/](https://aws.amazon.com/systems-manager/pricing/)
* User Guide - [https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)

## Installation

Follow the links provided here to get details regarding the installation of the SSM Agent on your specific operating systems.

[https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-manual-agent-install.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-manual-agent-install.html)

If you are comfortable with this procedure, jump to the Agent Installation section for your specific operating system from the menu on the left.

### Ubuntu Server

Pointers and tips for SSM installation on Ubuntu Server

#### Checking OS Version 

To get the current version, enter the following command:

```
$ lsb_release -a
```

The output should look something like this:

```
$ $ lsb_release -a
2 No LSB modules are available.
3 Distributor ID: Ubuntu
4 Description: Ubuntu 16.04.2 LTS
5 Release: 16.04
6 Codename: xenial
7 $
```

Your OS version is listed as the Description: Ubuntu 16.04.2

#### Checking System Architecture

To get the current architecture, enter the following command:

```
$ lscpu
```

The output should look something like this:

```
$ lscpu
2 Architecture: x86_64
3 CPU op-mode(s): 32-bit, 64-bit
4 Byte Order: Little Endian
5 CPU(s): 2
6 On-line CPU(s) list: 0,1
7 Thread(s) per core: 1
8 Core(s) per socket: 2
9 Socket(s): 1
10 NUMA node(s): 1
11 Vendor ID: GenuineIntel
12 CPU family: 6
13 Model: 63
14 Model name: Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
15 Stepping: 2
16 CPU MHz: 2400.048
17 BogoMIPS: 4800.09
18 Hypervisor vendor: Xen
19 Virtualization type: full
20 L1d cache: 32K
21 L1i cache: 32K
22 L2 cache: 256K
23 L3 cache: 30720K
24 NUMA node0 CPU(s): 0,1
25 Flag
```

Your architecture is listed as the Architecture: `x86_64`
