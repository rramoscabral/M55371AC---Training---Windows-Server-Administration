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


## Module 02: Identity services in Windows Server

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

## Module 05: Hyper-V virtualization and containers in Windows Server


- **Windows Containers [Docker Community Edition (CE)](https://docs.docker.com/desktop/install/windows-install/) / [Moby Project](https://mobyproject.org/)**

    ```powershell
    Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
    .\install-docker-ce.ps1
    ```

    <br/>

<br/>

---

<br/>



## Module 07: Disaster recovery in Windows Server

- **Implementing Hyper-V Replica**

    ```powershell

    #$cred=Get-Credential 

    $password = ConvertTo-SecureString "Pa55w.rd" -AsPlainText -Force
    $cred = New-Object System.Management.Automation.PSCredential ("Contoso\Administrator", $password)

    $sess = New-PSSession -Credential $cred -ComputerName sea-svr1.contoso.com 
    
    Enter-PSSession $sess 

    Get-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)" 

    Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"

    Get-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)" 

    Set-VMReplicationServer -ReplicationEnabled $true -AllowedAuthenticationType Kerberos -ReplicationAllowedFromAnyServer $true -DefaultStorageLocation c:\ReplicaStorage

    Get-VMReplicationServer

    RepEnabled:True AuthType:KerbKerAuthPort:80 CertAuthPort:443AllowAnyServer:True

    Get-VM 

    $sess1 = New-PSSession -Credential $cred -ComputerName sea-svr2.contoso.com 

    Enter-PSSession $sess1 

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

    New-ADOrganizationalUnit -Name "Seattle_Servers" Get-ADComputer SEA-SVR1 | Move-ADObject –TargetPath "OU=Seattle_Servers,DC=Contoso,DC=com"

    Msiexec /I C:\Labfiles\Mod08\LAPS.x64.msi

    Import-Module admpwd.ps 
    Update-AdmPwdADSchema 
    Set-AdmPwdComputerSelfPermission -Identity "Seattle_Servers"

    # SEA-SVR1

    Msiexec /I \\SEA-ADM1\c$\Labfiles\Mod08\LAPS.x64.msi

    gpupdate /force


    # SEA-ADM1

    Get-AdmPwdPassword SEA-SVR1 | Out-Gridview 
    ```

    <br/>

<br/>

---

<br/>



## Module 09: RDS in Windows Server


- **Install RDS using Windows Server PowerShell**

    ```powershell
    $SVR="SEA-RDS1.contoso.com"

    New-RDSessionDeployment -ConnectionBroker $SVR -WebAccessServer $SVR -SessionHost $SVR
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
