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

    Get-Service | Out-File '\\SEA-ADM1\C$\ServiceStatus.txt'
    ```

    <br/>

- **Create the Sales Managers group and add a user**

    ```powershell
    Enter-PSSession -ComputerName SEA-DC1

    New-ADGroup -Name "Sales Managers" -GroupCategory Security -GroupScope Global -DisplayName "Sales Managers" -Path "OU=Managers, DC=Contoso, DC=com" -Description "Sales Managers"

    Get-ADUser Ajay

    Get-ADGroup "CN=Sales Managers, OU=Managers, DC=Contoso, DC=com"

    Add-ADGroupMember -Identity "Sales Managers" -Members Ajay

    Get-ADGroupMember -Identity "Sales Managers" | fl
    ```

    <br/>

- **Configure Server Core**

    ```powershell
    # Change keyboard to en-US
    Set-WinUserLanguageList - LanguageList en-US -Force
    Set-Culture en-US

    # Change keyboard to pt-PT
    Set-WinUserLanguageList - LanguageList pt-PT -Force
    Set-Culture pt-PT


    # Remote Event Log Management
    Set-NetFirewallRule -DisplayGroup 'Remote Event Log Management' -Enabled True -PassThru | select DisplayName, Enable
    ```
    
    <br>


<br/>

---

<br/>


## Module 02: Identity services in Windows Server

- **Administrative templates**

    1. Download administrative templates (ADMX/ADL).
    2. Copy all **.admx** file to ``c:\Windows\SYSVOL\sysvol\Contoso.com\Policies\PolicyDefinitions``.
    3. Open **Group Policy Management**.
    4. Create or edit an existing GPO.
    5. Check **Computer Configuration > Policies > Administrative Templates** and **User Configuration > Policies > Administrative Templates**.
  
    <br>


<br/>

---

<br/>


## Module 03: Network infrastructure services in Windows Server

- **Create the IP Address Management (IPAM) GPOs**

    ```powershell
    
    Invoke-IpamGpoProvisioning -Domain contoso.com -GpoPrefixName IPAM -IpamServerFqdn sea-svr2.contoso.com 

    Get-GPO -All | FL DisplayName 
    ```

    <br>


<br/>

---

<br/>

## Module 04: File Servers and Storage management in Windows Server


- **Create a new mirrored volume with Diskpart**

    ```bash

    Enter-PSSession SEA-SVR3

    diskpart

    List disk
   
    Select disk 1
   
    attributes disk clear readonly
    
    online disk noerr
    
    Convert dynamic
    
    Select disk 2

    attributes disk clear readonly
    
    online disk noerr
    
    Convert dynamic

    create volume mirror disk=1,2
   
    format fs=ntfs quick label "Mirrored Volume"
    
    Assign letter=M:
    ```

    <br/>

- **Break mirror**

    ```bash
    C:\labfiles\mod04\CreateLabFiles.cmd \\sea-SVR3\Corpdata

    M:

    Cd corpdata

    Dir
    
    diskpart
  
    List volume

    Select volume M
    
    Break disk=2
    
    Exit
   
    Dir
    ```
    <br/>


- **Create an SMB share by using Windows PowerShell Remote**

    ```powershell
    Enter-PSSession -ComputerName SEA-SVR3

    Mkdir M:\Shares\SalesShare2
   
    New-SmbShare -Name SalesShare2 -Path M:\Shares\SalesShare2 -FolderEnumerationMode AccessBased

    Get-SmbShare
 
    Get-SmbShare SalesShare2 | FL
    ```

<br/>




---

<br/>

## Module 05: Hyper-V virtualization and containers in Windows Server

- **Install Docker on Windows Server**

    * [Docker Community Edition (CE)](https://docs.docker.com/desktop/install/windows-install/)
    * [Moby Project](https://mobyproject.org/)

   ```powershell

    Enter-PSSession -ComputerName SEA-SVR1

    Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1

    ./install-docker-ce.ps1

    Restart-Computer -ComputerName SEA-SVR1 -Force 

    Enter-PSSession -ComputerName SEA-SVR1

    ./install-docker-ce.ps1

    docker --version

    ```


    <br/>

- **Download and run a Windows container**

    ```powershell
    Docker images
    
    Docker search Microsoft
    
    docker container run hello-world:nanoserver
    
    # Nano Server (https://hub.docker.com/r/microsoft/windows-nanoserver)
    # Microsoft Artifact Registry (https://mcr.microsoft.com/)
    docker pull mcr.microsoft.com/windows/nanoserver:1809
    docker pull mcr.microsoft.com/windows/nanoserver:ltsc2019

    Docker images

    # Interactive mode
    Docker run -it --name NanoImage mcr.microsoft.com/windows/nanoserver:1809 -rm hostname

    docker run -it mcr.microsoft.com/windows/nanoserver:ltsc2022 -rm hostname

    # Hyper-V isolation mode
    Docker run -it --name NanoHVImage --isolation=hyperv mcr.microsoft.com/windows/nanoserver:1809

    hostname

    exit
    ```



<br/>

---

<br/>


## Module 06: High Availablity in Windows Server

-- **Validate and create a failover cluster**

    ```powershell
    Install-WindowsFeature -ComputerName SEA-SVR2 -Name Failover-Clustering -IncludeManagementTools
    Install-WindowsFeature -ComputerName SEA-SVR3 -Name Failover-Clustering -IncludeManagementTools

    Test-Cluster SEA-SVR2, SEA-SVR3 

    New-Cluster -Name WFC2022 -Node sea-svr2 -StaticAddress 172.16.10.125 

    Add-ClusterNode -Name SEA-SVR3 
    ```

    <br>



<br/>

---

<br/>


## Module 07: Disaster recovery in Windows Server

- **Implementing Hyper-V Replica**

    ```powershell



    # Create credentials for SEA-SVR1 and SEA-SVR2
    #$cred=Get-Credential 

    $password = ConvertTo-SecureString "Pa55w.rd" -AsPlainText -Force
    $cred = New-Object System.Management.Automation.PSCredential ("Contoso\Administrator", $password)


    # SEA-SVR1 as a Replica server for Hyper-V Replica
    $sess1 = New-PSSession -Credential $cred -ComputerName sea-svr1.contoso.com 
    
    Enter-PSSession $sess1

    Get-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)" 

    Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"

    Get-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)" 

    # SEA-SVR1 as a Replica server for Hyper-V Replica
    Set-VMReplicationServer -ReplicationEnabled $true -AllowedAuthenticationType Kerberos -ReplicationAllowedFromAnyServer $true -DefaultStorageLocation c:\ReplicaStorage

    Get-VMReplicationServer

    # SEA-CORE1 VM
    Get-VM 

    Exit


    # SEA-SRV2 for Hyper-V Replica
    $sess2 = New-PSSession -Credential $cred -ComputerName sea-svr2.contoso.com 

    Enter-PSSession $sess2 

    Install-WindowsFeature -Name Hyper-V, Hyper-V-PowerShell -Restart

    Enter-PSSession $sess2 

    Get-VM

    Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"

    Set-VMReplicationServer -ReplicationEnabled $true -AllowedAuthenticationType Kerberos -ReplicationAllowedFromAnyServer $true -DefaultStorageLocation c:\ReplicaStorage

    Get-VMReplicationServer

    Enable-VMReplication SEA-CORE1 -ReplicaServerName SEA-SVR2.contoso.com -ReplicaServerPort 80 -AuthenticationType Kerberos -computername SEA-SVR1.contoso.com 

    Start-VMInitialReplication SEA-CORE1 

    Get-VMReplication

    ```


<br/>

---

<br/>

## Module 08: Windows Server security


- **Locate problematic accounts**

    ```powershell
    New-ADUser -Name "JamesBrown" -OtherAttributes @{'title’="manager";'mail’="james.brown@contoso.com"} –PasswordNeverExpires:$true –AccountPassword (ConvertTo-SecureString -String "Pa55w.rd" -AsPlainText -Force ) –Enabled:$true -verbose 

    Get-ADUser -Filter {Enabled -eq $true -and PasswordNeverExpires -eq $true}

    $days = (Get-Date).Adddays(-90) Get-ADUser -Filter {LastLogonDate -lt $days -and enabled -eq $true} -Properties LastLogonDate

    #In this demo no accounts will be returned.
    ```

    <br/>


- **Configure and deploy LAPS**

    ```powershell

    # SEA-ADM1

    New-ADOrganizationalUnit -Name "Seattle_Servers" 
    
    Get-ADComputer SEA-SVR1 | Move-ADObject –TargetPath "OU=Seattle_Servers,DC=Contoso,DC=com"

    Msiexec /I C:\Labfiles\Mod08\LAPS.x64.msi

    Import-Module admpwd.ps 
    Update-AdmPwdADSchema 
    Set-AdmPwdComputerSelfPermission -Identity "Seattle_Servers"

    # Create LAPS_GPO
    gpmc.msc

    # SEA-SVR1 locally

    Msiexec /I \\SEA-ADM1\c$\Labfiles\Mod08\LAPS.x64.msi

    gpupdate /force


    # SEA-ADM1 

    Get-AdmPwdPassword SEA-SVR1 | Out-Gridview 
    ```

    <br/>


- **Connect to a JEA endpoint**

    ```powershell
    New-ADGroup -Name "DNSOps" -path "OU=IT,DC=Contoso,DC=com" -GroupScope Global 
     
    Get-ADGroup "DNSOps" | Add-ADGroupMember -Members (Get-AdUser -Filter 'name -like "Administrator"')

    Enter-PSSession SEA-SVR1

    Cd 'c:\Program Files\WindowsPowerShell\Modules’ 
    Mkdir DNSOps
    Cd DNSOps
    New-ModuleManifest .\DNSOps.psd1 
    Mkdir RoleCapabilities 
    Cd RoleCapabilities 
    New-PSRoleCapabilityFile -Path .\DNSOps.psrc 



    # Testing JEA in SEA-SVR1 

    $dnsopssession = New-PSSession -ComputerName SEA-SVR1 -ConfigurationName DNSOps 
    
    Import-PSSession -Session $dnsopssession -Prefix DNSOps 
    
    Get-DNSOpsCommand
    
    Enter-PSSession -Session $dnsopssession 
    
    Get-ComputerInfo

    Restart-Service W32Time
    
    Restart-Service DNS
    ```


- **Disable SMB 1.0, and configure SMB encryption on shares**

    ```powershell
    Enter-PSSession SEA-SVR1

    Set-SmbServerConfiguration –EnableSMB1Protocol $false 

    mkdir 'c:\labfiles\mod08' 
    
    New-SmbShare –Name 'Mod08' -Path 'c:\Labfiles\Mod08' –EncryptData $true 

    Grant-FileShareAccess –Name Mod08 -AccountName 'Everyone' -AccessRight Full

    # \\SEA-SVR1\mod08

    ```



<br/>

---

<br/>



## Module 09: RDS in Windows Server


- **Install RDS using Windows Server PowerShell**

    ```powershell
    Enter-PSSession -Session SEA-DC1
    
    $SVR="SEA-RDS1.contoso.com"

    New-RDSessionDeployment -ConnectionBroker $SVR -WebAccessServer $SVR -SessionHost $SVR

    # The installation take approximately 5 minutes
    ```

    <br/>

<br/>

---

<br/>

## Module 11: Server and performance monitoring in Windows Server


- **GUI-based tools launch from the command prompt**

    | GUI-based tools                   | command prompt |
    | ---                               | --- | 
    | Task Manager                      | TaskMgr.exe |
    | Performance Monitor               | PerfMon.exe |
    | Resource and Performance Monitor  | ResMon.exe |
    | Reliability Monitor               | PerfMon.exe /rel | 
    | Event Viewer                      | EventVwr.msc |
    | Server Manager                    | ServerManager.exe |


    <br/>
