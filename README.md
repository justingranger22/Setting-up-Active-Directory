# Setting-up and Using Active-Directory
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

Active Directory Deployed in the Cloud (Azure)</h1>

This tutorial is how to setup and use Active Directory 




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 Setting up Active Directory
- Step 2 Creating an Organizational Unit for Employees/Administrative users
- Step 3 Adding Employees to Security Groups
- Step 4 Connecting Users to the Domain
- Step 5 Setup Remote Desktop for Non-administrative Users
- Step 6 Group Policy and Managing Accounts

<h2>Deployment and Configuration Steps</h2>

<p>
  
![image](https://github.com/user-attachments/assets/6f51b386-b551-4cac-80b2-0de7837b7f93)
![image](https://github.com/user-attachments/assets/3786f78c-4933-46d0-9679-e160e4ac5b52)
To setup Active Directory you need to go to the Server Manager under the domain controller and click add roles and features, click next until you see server selection and make sure you have the domain controller selected (it should be the only one available), click next, check the box labeled Active Directory Domain Services, click add features, the click next until the confirmation tab, select the restart server automatically if required, say yes, then install. Once you completed the last part click on the flag in the upper right hand corner, select promote this server to a domain controller, click add new forest. Type in a domain name (it can be whatever you want, just make sure you write it down for use later). Next create a password (you might not need this in the future but write it down just in case), keep clicking next until you see DNS options and make sure the create DNS delegation box is UNCHECKED. Keep clicking next until you reach the prereq check, then click install. This will take some time and the desktop will restart once the installation is complete. Log back into the domain controller using the new forest domain you created (very important). Make sure you use the correct slash \ (DO NOT USE / ) as the system will not let you log in otherwise. This is because you need to tell the computer what context you want to be under (example log in as a domain user or domain admin as they have differnt permissions they can do)
</p>
<p>

</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/18758d66-803e-469f-833d-95f1a6bb6409)

This next set of steps is what you will be doing at a job creating units for the employees to help with organization and makes it easier without having to do them one at a time. To create an organizational unit click start, windows admin tools, active directory users and computers. Once opened, right click the domain (this is the forest you created earlier in the last slide), select new, organizational unit. Then you need to make sure you type EXACTLY what you see on this slide (even the underscore) which is _EMPLOYEES. Do the same for admins (_ADMINS). You can name them whatever you want and at your job they will vary but if your looking to practice its easier to simplify and the underscore helps since when you refresh those will be relocated to the top instead of by letter since characteristics come before letters when refreshing. To create admins/employees, double click the folder and select new, then user. Create the user (Jane or John Doe for example), select next, then create a password (remember for later use). Also for good practice make sure the first box is checked since this will force the new user to create a new password when they log in for the first time since you will be giving them a temporary password until they log in. DO NOT CHECK the other boxes since most are not good to do (you can delete/deactivate the user later)
</p>

![image](https://github.com/user-attachments/assets/ee0d6e74-d455-423c-bd3a-b2e76db58161)

To actually add the admins/employees to the correct security group, right click their name, select properties, member of, then type domain admins. This will change them from domain users to domain admins which is very important as admins have more authority than users do so be careful who you put under admins when at your job. Make sure you click check names so the system can put them in the correct group. Once they are in the correct group, go ahead and click apply, then ok. Try to log in as the new admin you created (in this example it would be domain.com\jane_admin and whatever password you created with the account)

</p>

![image](https://github.com/user-attachments/assets/0c223d89-57c0-40ce-8d56-0ff9e1716114)
Now that you created the domain and admin account, you can now link the user account to the domain account. To do this, go to settings, search about my pc, select rename this pc, click the change tab, select member of and type the domain you created (example mydomain.com). You will then have to type in the admin user and password (mydomain\jane_admin for this example). If done correctly you will get a welcome notification, if not there will be an error message because you typed something in wrong. You will then the prompted to restart the desktop so go ahead and restart the desktop. To check and see if it is connected go the domain admin account and go to active directory users and computers. Select the computer folder and the user account should be in there.
<br />
![image](https://github.com/user-attachments/assets/3d74c6d0-251b-437c-9e96-f88eabf16c5e)
To setup the user accounts to log into any of the computers in the same domain, go to settings, remote desktop, select users that can remotely access this pc (located in blue text at the bottom), click add, then type domain users (no need for admins here since they can do this already by default). Make sure you click check names so the system can find them (should be underlined). Go ahead and click ok to both.

![image](https://github.com/user-attachments/assets/3659b4a5-e49d-4de9-813e-0b350281de13)

You may have to create a group policy in order to fix lockout issues. To do this, right click start, run, type in gpmc.msc, press enter. This will open Group Policy Management Console. Right click Default Domain Policy, edit, group policy management, computer configuration, policies, window settings, security settings, account policies, account lockout policy. Once there you should see four policies that you can edit, choose one and change the setting (the others should change automatically). Click ok and apply. Test a user account to see if this works. Another way to check is to click on Default Domain Policy. Select the settings tab (click the close on the pop up screen) and scroll down and you should see the policy settings that you made.

![image](https://github.com/user-attachments/assets/169b6828-5bc6-48cc-856b-0642a68baff6)

To do any of the following (unlock account, change password, deactivate account) go to Active Directory Users and Computers under the admin account, click on the employee or right click and select properties, select account and to unlock the account check the unlock account box. The other options are underneath in the list (deactivate account or user must change password). To reset their password, right click on the employees name (if you need to search for them, look for Find Objects in Active Directory Domain Services then type the employees name) and select reset password. Type in a temporary password, select user must change password at next login (like if you were to create a new account). You can also unlock the account and disable the account as well by right clicking the employees name.
