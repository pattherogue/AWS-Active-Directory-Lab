# AWS Active Directory

## Objective
The AWS Active Directory project focused on setting up and managing a comprehensive Active Directory environment within AWS. The objective was to simulate a business environment by configuring Active Directory services on a Windows Server instance hosted in AWS. This project demonstrates key IT skills such as user management, organizational unit creation, and group policy administration, crucial for an entry-level help desk role.

### Skills Learned
- **Active Directory Management**: Proficient in configuring and managing Active Directory Domain Services (AD DS), including creating and managing organizational units (OUs) and user accounts.
- **Bulk User Management**: Experienced in using PowerShell for scripting and automating bulk user creation and management tasks.
- **Server and Network Configuration**: Skilled in setting up and configuring Windows Server on AWS, including network settings and security configurations.
- **Client Integration**: Competent in integrating client machines with Active Directory and ensuring domain connectivity.
- **Group Policy Management**: Adept at creating and managing Group Policy Objects (GPOs) to enforce domain-wide settings.
- **Troubleshooting and Support**: Enhanced problem-solving skills by addressing and resolving common issues related to domain login and Active Directory management.

### Tools Used
- **AWS**: Utilized AWS for deploying and managing Windows Server instances and network settings.
- **Active Directory Domain Services (AD DS)**: Implemented and managed domain services, crucial for user and domain management.
- **PowerShell**: Automated bulk user creation and management, showcasing proficiency in scripting.
- **Group Policy Management**: Configured domain-wide settings using Group Policy Objects (GPOs).
- **Windows Server Tools**: Employed various tools for server and network configuration, essential for IT support.

## Steps
### AWS Account Setup
*Ref 1: AWS EC2 Dashboard*

- **Setup**: Launched a t2.micro EC2 instance with Windows Server 2022 AMI.
  
  - ![EC2 Dashboard 1](https://i.imgur.com/xf8A6qM.png)
  - ![EC2 Dashboard 2](https://i.imgur.com/8uQHfis.png)
  - ![EC2 Dashboard 3](https://i.imgur.com/2WdlqmK.png)
    
- **Configuration**: Adjusted security group settings to permit RDP traffic.
  - ![Security Group Settings](https://i.imgur.com/9m9DywS.png)
  - ![Security Group Settings](https://i.imgur.com/bXxEgqM.png)

### Active Directory Configuration
*Ref 2: AD DS Installation*

- **Installation**: Added the AD DS role and promoted the server to a Domain Controller.
  - ![AD DS Installation](https://i.imgur.com/qc9pHUz.png)
  - ![AD DS Installation](https://i.imgur.com/81OC7qo.png)
- **Management**: Created and managed users and organizational units (OUs).
  - ![AD DS Management](https://i.imgur.com/eiXTI3m.png)

### Bulk User Management
*Ref 3: PowerShell Script*

- **Automation**: Used PowerShell to import users from a CSV file and manage them in bulk.

   The following PowerShell script was used to create and manage users in bulk:

   ```powershell
   Import-Module ActiveDirectory
   $users = Import-Csv "C:\path\to\your\users.csv"
   foreach ($user in $users) {
       New-ADUser -Name $user.Name -GivenName $user.GivenName -Surname $user.Surname -SamAccountName $user.Username -UserPrincipalName "$($user.Username)@yourdomain.local" -Path "OU=Users,DC=yourdomain,DC=local" -AccountPassword (ConvertTo-SecureString $user.Password -AsPlainText -Force) -PasswordNeverExpires $true -PassThru
   }


### Client Integration
*Ref 4: Domain Login Test*

- **Integration**: Connected a client machine to the domain and confirmed domain login and connectivity.
  - ![Domain Login Test](https://i.imgur.com/Yswttr0.png)
  - ![Domain Login Test](https://i.imgur.com/PYzltYQ.png)

### Group Policy Management
*Ref 5: GPO Creation*

- **Configuration**: Developed and managed Group Policy Objects (GPOs) for domain-wide settings.
  - ![GPO Creation](https://i.imgur.com/vDWaQuR.png)

### Troubleshooting and Support
*Ref 6: Issue Resolution*

- **Resolution**: Addressed and solved common issues related to domain login and Active Directory, demonstrating essential help desk problem-solving skills.

- **Description of Issues Encountered**:
  - During the configuration and management of the Active Directory environment, I encountered several common issues, such as domain login failures and permission errors.
  - For example, one issue involved users being unable to log in due to incorrect DNS settings. This was resolved by adjusting the DNS server configuration on the client machine to point to the correct IP address of the Domain Controller.

- **Steps Taken to Resolve Issues**:
  - To troubleshoot the login issue, I first checked the Event Viewer on both the client machine and the server for relevant error logs. The logs indicated that the client could not locate the domain because it was pointing to an incorrect DNS server.
  - I updated the client machine’s network settings to use the IP address of the Domain Controller as its primary DNS server. This change allowed the client to locate the domain and successfully authenticate users.
  - Additionally, I verified the Group Policy settings to ensure that they were being applied correctly across the domain.

- **Outcome**:
  - After applying the necessary changes, users were able to log in to the domain without further issues. The DNS configuration changes ensured that the client machines could consistently resolve the domain name, leading to successful logins and improved connectivity within the domain.
