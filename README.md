# **Design and Implement a Virtual Network in Azure**
<br>
<br>
This repository contains my solution for the Microsoft Learn exercise “Design and implement a virtual network in Azure”. The goal is to plan and implement multiple Azure Virtual Networks (VNets) and subnets based on a scenario for Contoso Ltd.

---
[Module link: Introduction to Azure Virtual Networks – Exercise](https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-virtual-networks/4-exercise-design-implement-virtual-network-azure)
---
# Overview

In this exercise, I designed and implemented VNets across multiple regions to support different workloads.

Skills demonstrated:

Creating Azure Resource Groups
Designing VNets with subnets
Implementing and verifying VNets in Azure Portal
Using Azure CLI for network automation
🗺 Architecture Diagram (Mermaid)

<img width="8191" height="1626" alt="Core Services Network-2026-04-13-175953" src="https://github.com/user-attachments/assets/9a04002e-65cd-4f01-8e85-936bc2e06fbc" />

Figure 1: Azure VNets, subnets, and optional peering connections

---

# Prerequisites

Before starting this exercise, make sure you have:

An active Azure subscription
Basic knowledge of IP addressing and subnetting
Familiarity with Azure Portal
🛠 Implementation Steps

---

# 1️. Create Resource Group
Resource Group Name: ContosoResourceGroup
Location: East US

<img width="1654" height="442" alt="image" src="https://github.com/user-attachments/assets/07c4a60c-ea40-4db6-8fbf-1ac97088bc1f" />


Figure 2: ContosoResourceGroup created in Azure Portal

---

# 2️. Create CoreServicesVnet
Address Space: 10.20.0.0/16
Region: East US
Subnets:
GatewaySubnet – 10.20.0.0/27
SharedServicesSubnet – 10.20.10.0/24
DatabaseSubnet – 10.20.20.0/24
PublicWebServiceSubnet – 10.20.30.0/24

<img width="1870" height="447" alt="image" src="https://github.com/user-attachments/assets/07b09e7d-6f7e-4311-b376-d181627f951b" />


Figure 3: CoreServicesVnet with subnets

Azure CLI / PowerShell Commands:
```
PS> az group create --name ContosoResourceGroup --location eastus
PS> az network vnet create --resource-group ContosoResourceGroup --name CoreServicesVnet --address-prefix 10.20.0.0/16 --subnet-name GatewaySubnet --subnet-prefix 10.20.0.0/27
PS> az network vnet subnet create --resource-group ContosoResourceGroup --vnet-name CoreServicesVnet --name SharedServicesSubnet --address-prefix 10.20.10.0/24
PS> az network vnet subnet create --resource-group ContosoResourceGroup --vnet-name CoreServicesVnet --name DatabaseSubnet --address-prefix 10.20.20.0/24
PS> az network vnet subnet create --resource-group ContosoResourceGroup --vnet-name CoreServicesVnet --name PublicWebServiceSubnet --address-prefix 10.20.30.0/24
```

---

# 3️. Create ManufacturingVnet
Address Space: 10.30.0.0/16
Region: West Europe
Subnets:
ManufacturingSystemSubnet
SensorSubnet1
SensorSubnet2
SensorSubnet3

<img width="1369" height="424" alt="image" src="https://github.com/user-attachments/assets/c2dc4d6b-cd1c-4384-9f5e-f34d31c5e1b3" />



Figure 4: ManufacturingVnet and its subnets

Azure CLI / PowerShell Commands:
```
PS> az network vnet create --resource-group ContosoResourceGroup --name ManufacturingVnet --address-prefix 10.30.0.0/16 --subnet-name ManufacturingSystemSubnet --subnet-prefix 10.30.0.0/24
PS> az network vnet subnet create --resource-group ContosoResourceGroup --vnet-name ManufacturingVnet --name SensorSubnet1 --address-prefix 10.30.10.0/24
PS> az network vnet subnet create --resource-group ContosoResourceGroup --vnet-name ManufacturingVnet --name SensorSubnet2 --address-prefix 10.30.20.0/24
PS> az network vnet subnet create --resource-group ContosoResourceGroup --vnet-name ManufacturingVnet --name SensorSubnet3 --address-prefix 10.30.30.0/24
```
---

# 4️. Create ResearchVnet
Address Space: 10.40.0.0/16
Region: Southeast Asia
Subnet: ResearchSystemSubnet

<img width="1452" height="415" alt="image" src="https://github.com/user-attachments/assets/9eddc458-e0da-44d8-b21d-7929bc0d9f8c" />



Figure 5: ResearchVnet subnet setup

Azure CLI / PowerShell Commands:

```
PS> az network vnet create --resource-group ContosoResourceGroup --name ResearchVnet --address-prefix 10.40.0.0/16 --subnet-name ResearchSystemSubnet --subnet-prefix 10.40.0.0/24
```
---

# Verification

After creating all VNets and subnets:

Go to All Resources in Azure Portal
Confirm all VNets appear under the correct Resource Group
Click each VNet → Subnets tab to verify subnet names and address ranges

<img width="1721" height="430" alt="image" src="https://github.com/user-attachments/assets/4740130e-b343-4531-ab41-0bd534b402da" />


---

 # Outcomes
- Resource Group created
- CoreServicesVnet and subnets created
- ManufacturingVnet and subnets created
- ResearchVnet and subnet created
- Resources verified in Azure Portal

---
 
# References
[Microsoft Learn: Design and implement a virtual network in Azure](https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-virtual-networks/4-exercise-design-implement-virtual-network-azure)
