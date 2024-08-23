Useful Windows Commands

Useful Windows Commands


To create a system state backup and store it on volume f, type:
wbadmin start systemstatebackup -backupTarget:f:


POWERSHELL: FIX BROKEN TRUST
Logged in as local admin via elevated PowerShell:
$cred = Get-Credential
Test-ComputerSecureChannel -Credential $cred -Repair

Get the wifi password from a machine that's already on the wifi but the password is unknown

netsh wlan show profile name="UNA_Guest" key=clear

Find Locked Accounts in power shell
Search-ADAccount -LockedOut

Get the product keys from the registry if you're re-installing and don't have the keys from the packaging. 

(Get-WmiObject -query 'select * from SoftwareLicensingService').OA3xOriginalProductKey

The report it outputs will show you which on-premises accounts are synchronized to the cloud.

Import-Module ActiveDirectory
Connect-AzureAD

Get-ADUser -Filter {Enabled -EQ $True} -Properties *  | 
    Select-Object DisplayName, SamAccountName, UserPrincipalName, LastLogonDate,           
    @{N="AzureADSynced"; E={(Get-AzureADUser -ObjectID $_.UserPrincipalName |
    Select-Object -Property DirSyncEnabled).DirsyncEnabled}} | 
Export-Csv $env:userprofile\documents\On-Prem_CloudSynced_Accounts.csv

Three must have powershell commands

get-help
get-command

get-member. show data structure of command. eg: get-service | get-member

Get all users password reset date. 

get-aduser -filter * -properties passwordlastset

Single user last password reset date

get-aduser <username> -properties passwordlastset

All users with formatting by date. 

“Get-ADUser -Filter * -Properties PasswordLastSet | Sort-Object -Property PasswordLastSet | Select-Object Name, PasswordLastSet”

AD Health checks

netdom query FSMO > fsmo.txt
netdiag /v /l > http://netdiag.tt
dcdiag /e /c /v /f:dcdiag.log
dcdiag.exe /TEST:RidManager /v /f:ridpool.log | find /i "Available RID Pool for the Domain"
repadmin /failcache > failcache.log 
repadmin / istg > istg.log 
repadmin /latency > latency.log 
repadmin /queue > queue.log
repadmin /showconn > showconn.log
repadmin /showrepl > showrepl.log
repadmin /replsummary > replsummary.log
dnslint /ad 10.6.0.4 /s 10.6.0.4 /v 
gpotool / domain:domain.local /checkacl /verbose > gpotool.log
w32tm /monitor > w32tm.log

