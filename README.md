<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1> Active Directory Network Files Shares and Permissions (Azure)</h1>
This tutorial outlines the implementation of sharing out resources over the network and creating file shares to allow Read, Write or Deny access to individual users or groups.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>File Sharing and Configuring Permissions Process</h2>

- Create file shares with various permissions. 
- Attempt to access file shares as a normal user.
- Create a Security Group assign permissions and test access. 

<h2>Create file shares with various permissions</h2>

<p>
<img width="442" alt="Capture1" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/ee253f28-8e9a-488c-a161-4263ca95c64c">
</p>
<p>
We connected to the server DC-1. On the C:\ drive, we created four folders: "read-access", "write-access", "no-access" and "accounting."
</p>
<br />

<p>
<img width="402" alt="Capture2" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/abcf1dd3-bca2-4236-bd94-0e26a5d00dcf">
</p>
<p>
We shared the folder "read-access" to the Domain Users group with the permission of "Read."
</p>
<br />

<p>
<img width="400" alt="Capture3" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/9aa767ef-f646-4838-84db-c7c39dda1230">
</p>
<p>
We shared the folder "write-access" to the Domain Users group with the permission of "Read/Write."
</p>
<br />

<p>
<img width="403" alt="Capture4" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/52a10423-3e6a-4d88-8d54-9a2777c936a3">
</p>
<p>
We shared the folder "no-access" to the Domain Admins group with the permission of "Read/Write." We skipped the accounting file. 
</p>
<br />

<h2>Attempt to access file shares as a normal user</h2>

<p>
<img width="418" alt="Capture5" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/2fa62c5e-e468-496a-9b1c-f83d957edef2">
</p>
<p>
From computer Client-1, we accessed the shared folder by navigating to its location on the network. Upon reaching the designated folders, we were able to view the shared files. Note: we logged in with an user with limited access privilage in the network. 
</p>
<br />

<p>
<img width="483" alt="Capture6" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/40131325-1caf-40fa-a09f-72bd87087c59">
</p>
<p>
The user has no access to the shared folder "no-access" becuase it is only limited to the Domain Admins group. 
</p>
<br />

<p>
<img width="455" alt="Capture10" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/8b49c0cd-a596-46d7-91c9-b4901ccc54e4">
<img width="406" alt="Capture11" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/e9d1134f-e42e-457e-b035-e825da43f572">
</p>
<p>
The user was able to read the contents of the shared folder "read-access" but is not able to edit this folder. 
</p>
<br />

<p>
<img width="446" alt="Capture8" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/06c5e161-2491-473b-9ad1-dbfbc9270069">
</p>
<p>
The user was able to edit the "write-access" folder by adding a text document to the shared folder. The file permissions are set to "Read/Write" for the Domain Users group. 
</p>
<br />

<h2> Create a Security Group assign permissions and test access</h2>

<p>
<img width="414" alt="Capture12" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/b67bd1aa-12f7-4033-8972-5408954c2039">
</p>
<p>
Going back to the server DC-1, on Active Directory Users and Computers, we created a security group called "ACCOUNTANTS."
</p>
<br />

<p>
<img width="400" alt="Capture13" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/cc3ce93b-be99-42d1-ad61-58da90f8f220">
</p>
<p>
On the "accounting" folder created earlier, we shared it wih the group "ACCOUNTANTS" with the permissions of "Read/Write."
</p>
<br />

<p>
<img width="482" alt="Capture14" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/1857fb24-0024-44f2-88e6-b3aac4ebd320">
</p>
<p>
From computer Client-1, we accessed the shared folder and clicked the accounting folder but we got access denied.
</p>
<br />

<p>
<img width="377" alt="Capture15" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/f76fc70b-25a7-433f-b053-100737b36a13">
</p>
<p>
The reason of the access denied is becuase the user is not part of the "ACCOUNTANTS" security group. On Active Directory User and Computers, we added user "saf.racu" to the "ACCOUNTANTS" security group and then logged out from computer Client-1.
</p>
<br />

<p>
<img width="406" alt="Capture16" src="https://github.com/gabromerorodriguez/FileShares-Permissions/assets/163021104/b943dda3-e74e-4034-af93-cdbdf4ff3c90">
</p>
<p>
We connected to computer Clint-1 again, this time the access to the shared folder "accounting" worked with "Read/Write" permissions.  
</p>
<br />

<h2></h2>
This lab documentation has provided a comprehensive understanding of Active Directory file share and permissions on the network. Through practical exploration and configuration exercises, we have gained insights into the fundamental concepts of file sharing, security settings, and access controls within an Active Directory environment. By effectively managing file shares and permissions, organizations can ensure data integrity, confidentiality, and accessibility, thereby enhancing collaboration and productivity across the network.
