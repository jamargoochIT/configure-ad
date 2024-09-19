![Microsoft Azure](https://github.com/user-attachments/assets/f4b437fc-74ac-462d-a6d4-71891ab3f156)


<h1>On-premises Active Directory Deployed in Azure</h1>
This tutorial goes through the implementation of on-premises Active Directory within Azure Virtual Machines.<br /><br><br><br><br>


<p>
After setting up DC-1 and Client-1 in Azure, we can install Active Directory on DC-1.
  
But before we do that, we should briefly go over what active directory is and some of its functions. (This is not a comprehensive explanation of Active Directory and all its functions.)
Active Directory is a centralized directory almost like a phone book, with usernames, passwords and permissions.
Some of Active Directory's fucntions are:<br>
- User Authentication – Checks credentials to make sure you’re allowed to access specific resources. 
- Group Management – Organizes users into groups to make it easier to manage policies and permissions.
- Policy Enforcement – Allows admins to create and set polices for users and computers.
- Network Organization – Hierarchical organization of forests, trees, domains, organizational units (Ous), and objects. 
- Forest – Top level – The entire hierarchical structure that everything else resides within or below.
- Trees – Collection of one or two domains that share a common namespace: Example, if you have a main domain named buy.com a tree would be returns.buy.com and sales.buy.com.
- Domains – Sub-divisions – A separate area within the forest, with its own users and resources.
- Organizational Units – Within domains, similar to folders that organize objects.
- Objects – Individual items - Users, computers, groups, OUs, and printers.<br><br>
 

Whew.<br><br>


Now, let’s get started by logging into DC-1 and in the server manager dashboard click on 2. Add roles and features.
![1](https://github.com/user-attachments/assets/e7bdf61b-d998-42e6-9d97-a18d182dffc8)<br><br><br><br>

 

In the installation window that opens up select next. 
![2](https://github.com/user-attachments/assets/fd7db18d-2655-49c1-95ee-30e89da375eb)<br><br><br><br>

 



 

Select Role-based or feature-based installation
Then click next.
![3](https://github.com/user-attachments/assets/cd2eadee-2069-41a3-8389-17d9f2e6c1b0)<br><br><br><br>



 

Select DC-1, which in our case should be the only option. We’ll click next.
![4](https://github.com/user-attachments/assets/3f318f6b-6e22-4774-9581-48c6f6145324)<br><br><br><br>


 

Now, we’ll select active directory domain services and click next.

![5](https://github.com/user-attachments/assets/5f391940-3630-4a31-b239-46d54dd7b225)<br><br><br><br>


 

Click Add features then click next.
![6](https://github.com/user-attachments/assets/49251153-ca32-4fd9-9e4c-c76a3421647e)<br><br><br><br>

 

Click next.
![7](https://github.com/user-attachments/assets/fdb41c92-0a04-41af-8bae-9d8935c399c3)<br><br><br><br>

 

Simply click next.
![8](https://github.com/user-attachments/assets/1f309862-5c59-4278-af16-eb116ae06a35)<br><br><br><br>

 

We’ll click the box to Restart the destination server automatically if required and we’ll get a confirmation window that opens up, we’ll click yes and finally click install.

![9](https://github.com/user-attachments/assets/13dc22dd-9b22-4b87-8019-2f22de4c6c1d)<br><br><br><br>


After the installation is complete, click close and go back to the server manager dashboard.

![10](https://github.com/user-attachments/assets/ead891c9-d861-4c1f-9d60-f19bf8d02b82)<br><br><br><br>


Now that Active directory is installed, we’re going to configure the DC-1 virtual machine to become a domain controller.


Click the flag in the upper right-hand corner and click promote this sever to domain controller.
![11](https://github.com/user-attachments/assets/5892c5f6-f9ef-49ec-a516-b920ec9ed4ae)<br><br><br><br>



In the deployment configuration window, we’ll click on add a new forest and then type in our name for it. In this example I named my forest mydomain.com. Click next.

![12](https://github.com/user-attachments/assets/c1ed23da-1515-4f8f-8594-1625baa24edd)<br><br><br><br>




On the domain controller window, we’re going to create a password and then click next.

![13](https://github.com/user-attachments/assets/4c3b36e5-3fbd-4197-8fe1-a224adc15362)<br><br><br><br>



We do not want to create a DNS delegation, so we have to make sure this box is unchecked before we click next.
![14](https://github.com/user-attachments/assets/4e8a1dbe-39fc-4d49-9e2e-339903f1fe8e)<br><br><br><br>



We’ll click next again.
![15](https://github.com/user-attachments/assets/535af41f-95bb-4fc7-a7e0-d56a0beabdb5)<br><br><br><br>


We’ll click next again
![16](https://github.com/user-attachments/assets/74c2bc9c-507f-43d7-80ae-8de0a1eb004e)<br><br><br><br>



Next again.
![17](https://github.com/user-attachments/assets/cbb5c0a4-8128-49a8-897f-32eb28307441)<br><br><br><br>


Now we can click install.
![18](https://github.com/user-attachments/assets/1a73f086-aab0-4b13-b0fb-5d7926f0d0b7)
When the installation is finished the VM will restart.<br><br><br><br> 


Now we’ll create a domain admin within the domain.

Since we’ve created a domain, if we want to log into that domain, we have to change our username at the login window to specify which domain we’d like to join. So, our username would look like this: mydomain.com\username. In this example, the username I set up is labuser. The password will still be the same one we used without the domain name added onto our username.
![19](https://github.com/user-attachments/assets/157f2ca3-0b0e-47c2-9949-9854756dcb69)<br><br><br><br>



In the windows search bar, type in active directory users and computers to open the application. Right click on mydomain.com and select new, then organizational unit.

![20](https://github.com/user-attachments/assets/015855aa-888b-4f34-b011-477895d9dc7f)<br><br><br><br>



Name the organizational unit Employees, then click okay.
We’ll follow the same process to create another OU named Admins.
![21](https://github.com/user-attachments/assets/ecd9dab2-f046-4a23-9876-1f311c69aadb)<br><br><br><br>


We’ll right click on the Admins OU and select new.
We’ll fill out the fields, (you don’t need to fill in the last name field.) then click next.
![22](https://github.com/user-attachments/assets/eced69c5-c6f8-42a5-a05f-971c5d807ded)<br><br><br><br>


We’ll create a password and select any of the options below if we want. 

![23](https://github.com/user-attachments/assets/52ab79aa-4037-43a4-b6e7-d3f04283c5f8)<br><br><br><br>




Click finish. Creating non-administrative users is done in the same way, but instead of using the Admin OU we’d use the Employees OU and not make them a member of the Domain Admins group.
![24](https://github.com/user-attachments/assets/2df5edb8-d2ce-4194-a9cc-5b08223535f5)<br><br><br><br>


When creating a user, simply adding admin to their name won’t do anything, adding them to the Domain Admins group gives them domain admin permissions. 
Domain Admins can manage an entire domain consisting of multiple computers all at once, while local admins are only able to manage a single machine at a time. 
Now, let’s right click on the admin we just created and select properties. At the top of the window click on the Member Of tab then click on add.

![25](https://github.com/user-attachments/assets/a8ec07ca-b815-4f05-95d3-e69965fa99c4)<br><br><br><br>



In the new window, type Domain Admins then click check name, click ok, click apply, and then ok.
![26](https://github.com/user-attachments/assets/27b4285e-bd25-4308-be5d-47143c775d43)<br><br><br><br>

![27](https://github.com/user-attachments/assets/de8f7ae3-e820-458e-b914-c406d10137e3)<br><br><br><br>



Now we’ll sign out of DC-1 and then sign in as the admin we just created to ensure that we can in fact log into the admin account.
![28](https://github.com/user-attachments/assets/f42323da-5f0f-40c9-a5d6-c2dacc34f555)<br><br><br><br>



Once we’ve logged in, we can move on to the next step. 
![29](https://github.com/user-attachments/assets/e37f68e1-722f-4e08-801c-19fea20b7a8c)<br><br><br><br>






Now, we’ll log back into Client-1 as the local admin, in my case labuser, the credentials we used without mydomain.com.
Once we’ve logged in, we’re going to right click on the windows start menu and select system.

![30](https://github.com/user-attachments/assets/d87b99df-a69b-4caa-8074-5ac3394cde0e)<br><br><br><br>



In the new window that opens, we’ll click on rename this PC (advanced).
![31](https://github.com/user-attachments/assets/a70b70bf-cefc-4e0c-a54a-0a42b5dfa8af)<br><br><br><br>

Click change.<br>
![32](https://github.com/user-attachments/assets/e77249e5-bfdc-4baf-a463-b4db20cdc5f4)<br><br><br><br>



Click Domain under Member Of.

![33](https://github.com/user-attachments/assets/80511dc7-a5d6-4489-98e3-f443d76fdfd4)<br><br><br><br>



Type in mydomain.com or what name you chose.

![34](https://github.com/user-attachments/assets/139cda25-ae95-46d2-a96d-d2291a82ce7e)<br><br><br><br>


Since we already set up Client-1 to use DC-1 as a DNS server, Client-1 is able to locate DC-1 and enable us to join its domain. If we didn’t do that, we’d get an error message stating that it couldn’t find the domain.
Now, we’ll type in the domain admin’s credentials we created in Active Directory.

![35](https://github.com/user-attachments/assets/ed9dd93a-44cb-460a-80b7-da559ad862af)<br><br><br><br>


Then click OK.<br>
![36](https://github.com/user-attachments/assets/0f91b5d9-4bd9-401f-997b-0a0a90a7299f)<br><br><br><br>


After you click OK, we’ll get a message stating that we’ll need to restart the Client-1 VM.
Click OK and then close.
![37](https://github.com/user-attachments/assets/d9f8e2ac-c2fd-4d82-b9b1-cec6db696295)<br><br><br><br>



We’ll be prompted to restart, so we’ll click restart now. After Client-1 restarts it will be a part of DC-1’s domain.<br><br><br>






Up next we’ll log into Client-1 as mydomain.com\dah_admin  (use what name you created.)

We’re going to open system properties by right clicking on the Windows start menu and selecting system.

![30](https://github.com/user-attachments/assets/8e00bdeb-9ce2-45f1-bcda-9187a54273bb)<br><br><br><br>




Now we’ll click on remote desktop.
<img width="906" alt="41" src="https://github.com/user-attachments/assets/5a4ca29f-4e91-4e49-9c7c-ff026d9789f9"><br><br><br><br>


Under User Accounts, click on select users that can remotely access this PC.

<img width="904" alt="42" src="https://github.com/user-attachments/assets/81e5c1bd-f308-407b-8fa7-af899a658614"><br><br><br><br>



In the window that opens, we’ll click on Add.

<img width="286" alt="43" src="https://github.com/user-attachments/assets/deaa8c77-a1a0-4b1d-9396-ad061d0ee7e6"><br><br><br><br>



Then we’ll type in Domain Users and click check name and then OK.<br>
<img width="352" alt="44" src="https://github.com/user-attachments/assets/da99301c-217b-4e28-a828-edf2bceee228"><br><br><br><br>


We have to configure this setting for non-admin users because we’re now joined to mydomain.com (As it says in the above image in the From this location field). So now, non-admin users can remote into the Client-1 computer (virtual machine).
We haven’t created any non-admin users (who would be found in the EMPLOYEES OU we created in active directory.) but if we had any they would be able to remote into Client-1 now.
And click OK again.

<img width="279" alt="45" src="https://github.com/user-attachments/assets/54c37f7b-ff8d-4351-801d-978c28386771"><br><br><br><br>



And that’s it. 











