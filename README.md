# EventIDs

| ID # | Short Desc   |	Description                                                                              |
| ---- | ------------ | ---------------------------------------------------------------------------------------- |
| 4624 | Logon Event	| Logon event, there are different types corresponding to the type of Login:               |
|      |              |  Logon Type                                                                              |
|      |              | 2 - Interactive - Logon via console
|      |              | 3 - Network - Network Logon
|      |              | 4 - Batch - Batch Logon (eg scheduled task)
|      |              | 5 - Service - Windows Service Logon
|      |              | 7 - Unlock -  Credentials used to unlock screen
|      |              | 8 - NetworkCleartext - Network Credentials (Cleartext - Logon with credentials sent in the clear text. 
|      |              | Most often indicates a logon to |IIS with "basic authentication)
|      |               | 9 - NewCredentials - Different Credentials other than logged on user 
|      |               | (NewCredentials such as with RunAs or |  |  mapping a network drive with | alternate credentials.  
|      |               | This logon type does not seem to show up in any events.  If you want to track users attempting to logon with 
|      |               | alternate credentials see 4648.  
|      |               | 10 - RemoteInteractive - (RDP)
|      |               | 11 - CachedInteractive - Cached Credentials  (Terminal Services, Remote Desktop or Remote Assistance)
|      |               | 12 - Cached Remote interactive (RDP - similar to 10)
|      |               | 13 - Cached Unlocked - (similar to type 7)
| 4625 | Failed Logon |	                                                                          
| 4648 | A logon was attempted using explicit credentials	A user connects to a server or runs a program locally using alternate credentials.  For instance a user maps a drive to a server but specifies a different user's credentials or opens a shortcut under RunAs by shift-control-right-clicking on the shortcut, selecting Run as..., and then filling in a different user's credentials in the dialog box that appears.  Or a user logs on to a web site using new specific credentials.  That is the case above in the example - Administrator was logged on to the local computer and then accessed a SharePoint server sp01.icemail.com as rsmith@mtg.com.
This event is also logged when a process logs on as a different account such as when the Scheduled Tasks service starts a task as the specified user. Logged on user: specifies the original user account.
With User Account Control enabled, an end user runs a program requiring admin authority.  You will get this event where the process information is consent.exe.  Unfortunately Subject does not identify the end user.
Unfortunately this event is also logged in situations where it doesn't seem necessary.  For instance logging on interactively to a member server (Win2008 RC1) with a domain account produces an instance of this event in addition to 2 instances of 4624.
4778	 A session was reconnected to a Window Station	Windows logs this event when a user reconnects to a disconnected terminal server (aka Remote Desktop) session as opposed to a fresh logon which is reflected by event 4624.

This event is also logged when a user returns to an existing logon session via Fast User Switching.

You can distinguish between instances of this event associated with Fast User Switching and Remote Desktop by Client Name: and Client Address: which in the case of Remote Desktop will normally be different than the local computer.  The session name also indicates Remote Desktop with "RDP" as shown in the example.

With console logons and Fast User Switching the session name will be "Console" and Client Name and Address will be "unknown".
4672	Special privileges assigned to new logon	This event lets you know whenever an account assigned any "administrator equivalent" user rights logs on.  For instance you will see event 4672 in close proximity to logon events (4624) for administrators since administrators have most of these admin-equivalent rights.

So, this is a useful right to detecting any "super user" account logons.  Of course this right is logged for any server or applications accounts logging on as a batch job (scheduled task) or system service.  See Logon Type: on event ID 4624.  You can correlate 4672 to 4624 by Logon ID:.

Note: "User rights" and "privileges" are synonymous terms used interchangeably in Windows.
Untitled section
Some other ones

  
Logon failure events

0xC0000064 User name does not exist
0xC000006A User name is correct but the password is wrong
0xC0000234 User is currently locked out
0xC0000072 Account is currently disabled
0xC000006F User tried to logon outside his day of week or time of day restrictions
0xC0000070 Workstation restriction
0xC00000193 Account expiration
0xC0000071 Expired password
0xC0000133 Clocks between DC and other computer too far out of sync
0xC0000224 User is required to change password at next logon
0xC0000225 Evidently a bug in Windows and not a risk
0xC000015b "The user has not been granted the requested logon"

Logon sessions

4624 Successful Logon
 
4625	Failed Logon	Logon failure events

0xC0000064 User name does not exist
0xC000006A User name is correct but the password is wrong
0xC0000234 User is currently locked out
0xC0000072 Account is currently disabled
0xC000006F User tried to logon outside his day of week or time of day restrictions
0xC0000070 Workstation restriction
0xC00000193 Account expiration
0xC0000071 Expired password
0xC0000133 Clocks between DC and other computer too far out of sync
0xC0000224 User is required to change password at next logon
0xC0000225 Evidently a bug in Windows and not a risk
0xC000015b "The user has not been granted the requested logon"
 
4647 user initiated logon
4800 Workstation Locked
4801 Workstation unlocked
4802 Screen saver loaded
4803 Screen saver dismissed
4778 RDP reconnected
4779 RDP disconnected

User account changes

4720 Created
4722 Enabled
4723 User changed own password
4724 Privileged User changed this user’s password
4725 Disabled
4726 Deleted
4728 A member was added to a security-enabled global group
4738 Changed
4740 Locked out
4756 User added to security enabled universal group
4767 Unlocked
4781 Name change
 
Others
7030 - Service Creation Errors [system log]
7045 - Servvice creation [system log]
