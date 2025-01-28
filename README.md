<p align="center">
<img src="https://i.imgur.com/9JmwJSF.png" alt="osTicket logo"/>
</p>

<h1>Active Directory: Configuring Accounts and Resetting Passwords 🪟</h1>
In this last section of our Microsoft Active Directory lab, we run through the process of using the Group Policy Management Console to configure Account Lockout and Reset Policies, test our Policy Updates by actively breaching the Account Lock Policies and then Resetting the Account to be able to log back in. We also briefly look at the process of disabling/enabling an account and lastly, we review the Security Logs within Microsoft Event Viewer for our Client Machine and see the events that outline the failed login attempts and account disabled login attempts.

(Link Back to Main Project Contents Page is at the Bottom of this Repo)
<h2>Environments and Technologies Used</h2>

- Lenovo Ideapad 5 Pro 16gb AMD Ryzen 7
- Microsoft Azure Resource Group
- Microsoft Azure Windows 10 Pro version 22H2 - x64 Gen2 Virtual Machine
- Microsoft Azure Windows Server 22 Datacenter: Azure Edition - x64 Gen2 Virtual Machine

<h2>Operating Systems Used </h2>

- Local Windows 11 Home Version 21H2</b>
- Windows 10 Pro Version 22H2 Virtual Machine
- Windows Server 22 Datacenter: Azure Edition - x64 Gen2 Virtual Machine
  
<h2>List of Prerequisites</h2>

- Microsoft Azure Subscription
- Microsoft Azure Subscription Credit 

<h2>Installation, Setup, Resource Setup, Executing Functions</h2>
1. To begin configuring an Account Lockout Policy, we need to access the Group Policy Management Console for our Active Directory Domain via Active Directory. Here we can see our domain forest showing up within our GP Management Console.
</p>
<br />

<p>
<img src="https://i.imgur.com/rMqcpl7.png" alt="1"/>
</p>
<p>
2. As we navigate through the dropdown menus for our Domain Forest within Group Policy Management, we need to access the Group Policy Objects menu in order to create a new GPO. This GPO will contain the criteria we choose that will determine when and how a User gets locked out of their account and how long for. We are calling it "Account Lockout Policy" and will edit this in the next slide. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DQv0NMW.png" alt="2"/>
</p>
<p>
3. In order to edit our new "Account Lockout Policy" we need to access the Group Policy Management Editor and navigate to our "Account Lockout Policy" which will be in the Account Policies menu within Security Settings. From here we can edit the policy and choose our desired criteria for how an account will be locked out.
</p>
<br />

<p>
<img src="https://i.imgur.com/zi0gKGp.png" alt="3"/>
</p>
<p>
4. Here we can now see the settings we have chosen for our Account Lockout Policy. Based on this slide, a User can attempt to login 5 times with an incorrect password, they will be locked out for 30 minutes before they can reattempt to login, administrator accounts are also set to be subject to these settings and the account lockout counter is set to reset after 10 minutes.
</p>
<br />

<p>
<img src="https://i.imgur.com/u0ZXpdt.png" alt="4"/>
</p>
<p>
5. Back in our main Group Policy Management Console, we can see within the Account Policies section of our Default Domain Policy settings, the established settings for our Account Lockout Policy.
</p>
<br />

<p>
<img src="https://i.imgur.com/t7622R9.png" alt="5"/>
</p>
<p>
6. To ensure that our Group Policy Account Lockout settings have been updated, within our Client Machine we can run the command "gpupdate /force" which will update the settings for our Admin User "jane_admin"
</p>
<br />

<img src="https://i.imgur.com/N4HnORp.png" alt="6"/>
</p>
<p>
7. From the following slide we can see the result of the Policy Update and confirmation that the Computer Policy and User Policies have updated.
</p>
<br />

<p>
<img src="https://i.imgur.com/keZxwxw.png" alt="7"/>
</p>
<p>
8. Now we can move on and test whether our Account Lockout Policy has been enacted for our Client Machine. We can do this by simply attempting to log in with an incorrect password (for our test user "ful.wos") and if the Policy has successfully been applied, after 5 attempts we should receive a message telling us that the account has been locked.
</p>
<br />

<p>
<img src="https://i.imgur.com/zjfPTY3.png" alt="8"/>
</p>
<p>
9. In our Domain Controller, if we look at the User properties for our test user "ful.wos" we can see that the user is currently locked out in this Domain Controller. We can now choose to unlock the account and in this case we can tick the "Unlock account" box and choose for the password to never expire. 
</p>
<br />

<p>
<img src="https://i.imgur.com/l3n9Mxu.png" alt="9"/>
</p>
<p>
10. Once we have unlocked the account and logged back in we can see here confirmation that the account is now unlocked. Please note it is usually advised to choose the option that "User must change password at next logon" to ensure the security of the account and the organisation.
</p>
<br />

<img src="https://i.imgur.com/B3bJXxw.png" alt="10"/>
</p>
<p>
11. If we take a look at our User within their designated Organisational Unit we can see an icon that displays that their account has been disabled. We can do this by simply right-clicking the user and choosing to disable their account. 
</p>
<br />

<p>
<img src="https://i.imgur.com/6FHfbcR.png" alt="11"/>
</p>
<p>
12. Here we can see that if we attempt to log into a Disabled User Account we get the message that the User is currently disabled. We can reverse this by simply going back into our Domain Controller, accessing the user via their designated Organisational Unit and enabling their account from the same right-click menu.
</p>
<br />

<p>
<img src="https://i.imgur.com/w4JQIXJ.png" alt="12"/>
</p>
<p>
13. In the event of a potential Security Breach, we may want to examine further the details of the event to obtain more information. 

Perhaps we need to determine the exact date and time of the security breach or understand more about the system that the breach attempt took place on. We can access this information by opening up the Event Viewer application, clicking on the Windows Logs dropdown menu and clicking on Security. Within this menu we can then see all the Security Audits related to User Account Management and Logon tasks. 

Below we can see the 5 Security Audit failures that took place when we attempted to log into our test Users account with an incorrect password. For each event we can see that the Event Viewer will log the Security ID, Account Name, and the Reason for the Security Failure
</p>
<br />

<p>
<img src="https://i.imgur.com/8M5ZX4W.png" alt="13"/>
</p>
<p>
14. Here is the failed Security Audit for the login attempt when the test users account was disabled. As we can see the Event Viewer will give this particular reason for why the login failed. If we want to do further enquries into the Audit Failure, we can click into the "Details" menu which will give us more System and Event information about the subject, event and underlying processes. This information can also be displayed in XML View and can be exported if required for further inspection.
</p>
<br />

<p>
<img src="https://i.imgur.com/hvFl4sc.png" alt="14"/>
</p>
<p>
LINK BACK TO THE MAIN PROJECT CONTENTS PAGE - https://github.com/cyberwahid01/Azure-Compute-and-Networking
