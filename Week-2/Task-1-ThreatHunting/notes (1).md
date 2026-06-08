Log Name:      Security
Source:        Microsoft-Windows-Security-Auditing
Date:          6/1/2026 9:16:11 AM
Event ID:      4688
Task Category: Process Creation
Level:         Information
Keywords:      Audit Success
User:          N/A
Computer:      DESKTOP-4O08HP3
Description:
A new process has been created.

Creator Subject:
	Security ID:		DESKTOP-4O08HP3\Predator
	Account Name:		Predator
	Account Domain:		DESKTOP-4O08HP3
	Logon ID:		0x34131

Target Subject:
	Security ID:		NULL SID
	Account Name:		-
	Account Domain:		-
	Logon ID:		0x0

Process Information:
	New Process ID:		0x1f98
	New Process Name:	C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
	Token Elevation Type:	%%1937
	Mandatory Label:		Mandatory Label\High Mandatory Level
	Creator Process ID:	0x219c
	Creator Process Name:	C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
	Process Command Line:	

Token Elevation Type indicates the type of token that was assigned to the new process in accordance with User Account Control policy.

Type 1 is a full token with no privileges removed or groups disabled.  A full token is only used if User Account Control is disabled or if the user is the built-in Administrator account or a service account.

Type 2 is an elevated token with no privileges removed or groups disabled.  An elevated token is used when User Account Control is enabled and the user chooses to start the program using Run as administrator.  An elevated token is also used when an application is configured to always require administrative privilege or to always require maximum privilege, and the user is a member of the Administrators group.

Type 3 is a limited token with administrative privileges removed and administrative groups disabled.  The limited token is used when User Account Control is enabled, the application does not require administrative privilege, and the user does not choose to start the program using Run as administrator.
Event Xml:
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="Microsoft-Windows-Security-Auditing" Guid="{54849625-5478-4994-a5ba-3e3b0328c30d}" />
    <EventID>4688</EventID>
    <Version>2</Version>
    <Level>0</Level>
    <Task>13312</Task>
    <Opcode>0</Opcode>
    <Keywords>0x8020000000000000</Keywords>
    <TimeCreated SystemTime="2026-06-01T03:46:11.9155656Z" />
    <EventRecordID>2328</EventRecordID>
    <Correlation />
    <Execution ProcessID="4" ThreadID="408" />
    <Channel>Security</Channel>
    <Computer>DESKTOP-4O08HP3</Computer>
    <Security />
  </System>
  <EventData>
    <Data Name="SubjectUserSid">S-1-5-21-4162243629-46228999-2687383167-1001</Data>
    <Data Name="SubjectUserName">Predator</Data>
    <Data Name="SubjectDomainName">DESKTOP-4O08HP3</Data>
    <Data Name="SubjectLogonId">0x34131</Data>
    <Data Name="NewProcessId">0x1f98</Data>
    <Data Name="NewProcessName">C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe</Data>
    <Data Name="TokenElevationType">%%1937</Data>
    <Data Name="ProcessId">0x219c</Data>
    <Data Name="CommandLine">
    </Data>
    <Data Name="TargetUserSid">S-1-0-0</Data>
    <Data Name="TargetUserName">-</Data>
    <Data Name="TargetDomainName">-</Data>
    <Data Name="TargetLogonId">0x0</Data>
    <Data Name="ParentProcessName">C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe</Data>
    <Data Name="MandatoryLabel">S-1-16-12288</Data>
  </EventData>
</Event>