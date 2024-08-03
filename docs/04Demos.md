---
layout: default
title: 'Trainer demonstrations'
nav_order: 4
has_children: false
---

# Trainer demonstrations
{: .no_toc }


## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<br/>

---

<br/>

## Module 01: Windows Server Administration Overview 


- **Manage servers remotely**

    ```powershell
    Enter-PSSession -ComputerName SEA-DC1

    Get-Service -Name IISAdmin

    Get-Service -Name IISAdmin | Restart-Service

    Get-Service | Out-File \SEA-ADM1\C$\ServiceStatus.txt
    ```


<br/>

---

<br/>

## Module 05: Hyper-V virtualization and containers in Windows Server


- **Windows Containers [Docker Community Edition (CE)](https://docs.docker.com/desktop/install/windows-install/) / [Moby Project](https://mobyproject.org/)**

    ```powershell
    Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
    .\install-docker-ce.ps1
    ```

<br/>

---

<br/>




# Module 11: Server and performance monitoring in Windows Server


- **GUI-based tools launch from the command prompt**

    | GUI-based tools                   | command prompt |
    | ---                               | --- | 
    | Task Manager                      | TaskMgr.exe |
    | Performance Monitor               | PerfMon.exe |
    | Resource and Performance Monitor  | ResMon.exe |
    | Reliability Monitor               | PerfMon.exe /rel | 
    | Event Viewer                      | EventVwr.msc |
    | Server Manager                    | ServerManager.exe |