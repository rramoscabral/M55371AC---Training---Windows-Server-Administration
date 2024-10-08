---
layout: default
title: 'Course Syllabus'
nav_order: 3
has_children: false
---

# Course Syllabus
{: .no_toc }


## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<br/>

---

<br/>

## Module 1: Windows Server Administration Overview
This module describes how to distinguish different Windows Server editions and techniques for deployment, servicing and activation. The module also introduces Windows Server Core and compares it with the Desktop Experience version. The module describes tools and concepts for administering Windows Server, such as Windows Admin Center, PowerShell, and delegation of privileges.

<br>

After completing this module, students will be able to:
- Describe Windows Server as well as techniques for deployment, servicing and activation.
- Describe Windows Server Core, its specifics and ways to administer it.


<br/>

**Lessons**
- Overview of Windows Server administration principles and tools
- Introducing Windows Server
- Overview of Windows Server Core


<br/>

**Lab 1: Deploying and configuring Windows Server**
- Deploying and configuring Server Core
- Implementing and using remote server administration


<br/>

## Module 2: Identity Services in Windows Server
This module introduces identity services and describes Active Directory Domain Services (AD DS) in a Windows Server environment. The module describes how to deploy domain controllers in AD DS, as well as the Azure Active Directory (AD) and the benefits of integrating Azure AD with AD DS. The module also covers Group Policy basics and how to configure group policy objects (GPOs) in a domain environment. Finally, the modules describes the role of Active Directory certificate services and certificate usage.

After completing this module, students will be able to:
- Describe AD DS in a Windows Server environment.
- Deploy domain controllers in AD DS.
- Describe Azure AD and benefits of integrating Azure AD with AD DS



<br/>

**Lessons**
- Overview of AD DS
- Deploying Windows Server domain controllers
- Overview of Microsoft Entra ID
- Implementing Group Policy
- Overview of AD CS



<br/>

**Lab 1: Implementing Identity Services and Group Policy**
- Deploying new domain controller on Server Core
- Configuring Group Policy
- Deploying and using certificate services
- Explain Group Policy basics and configure GPOs in a domain environment
- Describe the role of Active Directory certificate services and certificate usage


<br/>

## Module 3: Network Infrastructure services in Windows Server
This module describes how to implement core network infrastructure services in Windows Server. The modules covers how to deploy, configure and manage DNS and IPAM. The modules also describes how to use Remote Access Services.

After completing this module, students will be able to:
- Describe, deploy and configure DHCP service.
- Deploy, configure and manage DNS.
- Describe, deploy and manage IPAM.

<br/>

**Lessons**
- Deploying and managing DHCP
- Deploying and managing DNS service
- Deploying and managing IPAM
- Remote Access Services in Windows Server

<br/>

**Lab 1: Implementing and configuring network infrastructure services in Windows Server**
- Deploying and configuring DHCP
- Deploying and configuring DNS
- Implementing Web Application Proxy


## Module 4: File Servers and Storage management in Windows Server
This modules describes how to configure file servers and storage in Windows Server. The module covers file sharing and deployment of Storage Spaces technology. The module describes how to implement data deduplication, iSCSI based storage in Windows Server, and finally, how to deploy DFS.

After completing this module, students will be able to:
- Implement sharing in Windows Server
- Deploy Storage Spaces technology
- Implement the data deduplication feature
- Implement iSCSI based storage
- Deploy and manage Distributed File System (DFS)

<br/>

**Lessons**
- Volumes and File Systems in Windows Server
- Implementing sharing in Windows Server
- Implementing Storage Spaces in Windows Server
- Implementing Data Deduplication
- Implementing iSCSI
- Deploying Distributed File System

<br/>

**Lab 1: Implementing storage solutions in Windows Server**
- Implementing Data Deduplication
- Configuring iSCSI storage
- Configuring redundant storage spaces
- Implementing Storage Spaces Direct


<br/>

## Module 5: Hyper-V virtualization and containers in Windows Server
This modules describes how to implement and configure Hyper-V VMs and containers. The module covers key features of Hyper-V in Windows Server, describes VM settings, and how to configure VMs in Hyper-V. Themodule also covers security technologies used with virtualization, such as shielded VMs, Host Guardian Service, admin-trusted and TPM-trusted attestation, and KPS.

After completing this module, students will be able to:
- Describe the key features of Hyper-V in Windows Server.
- Describe VM settings and deploy and configure VMs in Hyper-V.
- Explain the use of security technologies for virtualization.
- Describe and deploy containers in Windows Server.
- Explain the use of Kubernetes on Windows.

<br/>

**Lessons**
- Hyper-V in Windows Server
- Configuring VMs
- Securing virtualization in Windows Server
- Containers in Windows Server
- Overview of Kubernetes

<br/>

**Lab 1: Implementing and configuring virtualization in Windows Server**
- Creating and configuring VMs
- Installing and configuring containers



<br/>

## Module 6: High Availablity in Windows Server
This module describes current high availability technologies in Windows Server. The module describes failover clustering and considerations for implementing it, and how to create and configure failover clustering. The module also explains stretch clusters and options for achieving high availability with Hyper-V VMs.

After completing this module, students will be able to:
- Describe failover clustering and the considerations for implementing it.
- Create and configure failover clusters.
- Describe stretch clusters.
- Describe options to achieve high availability with Hyper-V VMs.

  
<br/>

**Lessons**
- Planning for failover clustering implementation
- Creating and configuring failover cluster
- Overview of stretch clusters
- High availability and disaster recovery solutions with Hyper-V VMs

<br/>

**Lab 1: Implementing failover clustering**
- Configuring storage and creating a cluster
- Deploying and configuring a highly available file server
- Validating the deployment of the highly available file server

<br/>

## Module 7: Disaster recovery in Windows Server
This module describes disaster recovery technologies in Windows Server and how to implement them. The module covers how to configure and use Hyper-V Replica and describes Azure Site Recovery. The module also covers how to implement Windows Server backup and describes the Azure Backup service.

After completing this module, students will be able to:
- Describe and implement Hyper-V Replica.
- Describe Azure Site Recovery.
- Describe and implement Windows Server backup.
- Describe the Azure Backup service.

<br/>

**Lessons**
- Hyper-V Replica
- Backup and restore infrastructure in Windows Server


<br/>

**Lab 1: Implementing Hyper-V Replica and Windows Server Backup**
- Implementing Hyper-V Replica
- Implementing backup and restore with Windows Server Backup


<br/>

## Module 8: Windows Server security
This module describes Windows Server security features and how to implement them. The module covers credentials used in Windows Server and explains how to implement privileged access protection. In addition to describing methods and technologies for hardening Windows Server security, the module explains how to configure Just Enough Administration (JEA) and how to secure SMB traffic. Finally, the module covers Windows Update, its deployment and management options.

After completing this module, students will be able to:
- Describe credentials used in Windows Server.
- Explain how to implement privileged access protection.
- Describe methods and technologies to harden security in Windows Server.
- Describe and configure Just Enough Administration (JEA).
- Secure SMB traffic in Windows Server.
- Describe Windows Update and its deployment and management options

<br/>

**Lessons**
- Credentials and privileged access protection
- Hardening Windows Server
- JEA in Windows Server
- Securing and analyzing SMB traffic
- Windows Server update management

#<br/>

**Lab 1: Configuring security in Windows Server**
- Configuring Windows Defender Credential Guard
- Locating problematic accounts
- Implementing LAPS

<br/>

## Module 9: RDS in Windows Server
This module describes key Remote Desktop Protocol (RDP) and Virtual Desktop Infrastructure (VDI) features in Windows Server. The modules covers how to deploy session-based desktops and describes personal and poled virtual desktops.

After completing this module, students will be able to:
- Describe Remote Desktop Services (RDS) in Windows Server.
- Describe and deploy session-based desktops.
- Describe personal and pooled virtual desktops.

<br/>

**Lessons**
- Overview of RDS
- Configuring a session-based desktop deployment
- Overview of personal and pooled virtual desktops

<br/>

**Lab 1: Implementing RDS in Windows Server**
- Implementing RDS
- Configuring Session Collection Settings and using RDC
- Configuring a virtual desktop template


<br/>

## Module 10: Remote access and web services in Windows Server
This module describes how to implement virtual private networks (VPNs), Network Policy Server (NPS), and Microsoft Internet Information Services (IIS). The module describes Always On VPN functionality, as well as how to configure NPS and Web Server (IIS) in Windows Server.

After completing this module, students will be able to:
- Describe VPN options in Windows Server.
- Describe Always On VPN functionality.
- Describe and configure NPS.
- Describe and configure Web Server (IIS).

<br/>

**Lessons**
- Implementing VPNs
- Implementing Always On VPN
- Implementing NPS
- Implementing Web Server in Windows Server


<br/>

**Lab 1: Deploying network workloads**
- Implementing VPN in Windows Server
- Deploying and Configuring Web Server


<br/>

## Module 11: Server and performance monitoring in Windows Server
This module describes how to implement service and performance monitoring, and apply troubleshooting in Windows Server. The module highlights monitoring tools and describes how to monitor performance, including event logging and how to perform event logging monitoring for troubleshooting purposes.

After completing this module, students will be able to:
- Describe monitoring tools in Windows Server.
- Describe performance monitoring and use it in Windows Server.
- Describe event logging and perform event logging monitoring for troubleshooting purposes

<br/>

**Lessons**
- Overview of Windows Server monitoring tools
- Using Performance Monitor
- Monitoring event logs for troubleshooting

<br/>

**Lab 1: Monitoring and troubleshooting Windows Server**
- Establishing a performance baseline
- Identifying the source of a performance problem

<br/>

## Module 12: Upgrade and migration in Windows Server
This module describes how to perform upgrades and migrations for AD DS, Storage, and Windows Server. The module covers tools to use for AD DS migration. The module also covers the Storage Migration Service, and finally, Windows Server migration tools and usage scenarios.

After completing this module, students will be able to:
- Describe tools to use for AD DS migration.
- Describe the Storage Migration Service.
- Describe Windows Server migration tools and their usage scenarios

<br/>

**Lessons**
- AD DS migration
- Storage Migration Service
- Windows Server migration tools

<br/>

**Lab 1: Migrating Server workloads**
- Implementing Storage Migration Service
