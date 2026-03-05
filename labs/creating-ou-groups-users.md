# Creating-OU-Groups-Users
Active Directory Step-by-Step Tutorial (lab.local)

## Skills Demonstrated

- Active Directory Organizational Unit (OU) design
- User account provisioning and management
- Security and distribution group configuration
- Role-based access control using group membership
- Enterprise-style directory structure design
---

## Goal

Build a multi-region Active Directory structure and practice common identity tasks:

- Create regional **Organizational Units (OUs)** for **USA, Europe, Asia**
- Add sub-OUs for **Users, Computers, Servers, Groups**
- Create **security** and **distribution** groups in each region
- Create a test user (**Sam Pak**) and assign group memberships

---

## Environment

- **Domain:** `lab.local`
- **Domain Controller:** `DC01`
- **OS:** Windows Server 2022
- **Tool:** Active Directory Users and Computers (ADUC)

---

## Step 1 — Open Active Directory Users and Computers (ADUC)

1. On `DC01`, open **Server Manager**
2. Click:

   **Tools → Active Directory Users and Computers**

3. In the left pane, expand your domain:

   `lab.local`

---

## Step 2 — Create Regional OUs (USA, Europe, Asia)

You created three top-level OUs directly under the domain.

For each region:

1. Right-click **lab.local**
2. Select:

   **New → Organizational Unit**

3. Enter the OU name:
   - `USA`
   - `Europe`
   - `Asia`

4. Leave **Protect container from accidental deletion** checked
5. Click **OK**

✅ Result:  
lab.local  
├── USA  
├── Europe  
└── Asia  


---

## Step 3 — Create Sub-OUs Inside Each Region

Inside **USA**, **Europe**, and **Asia**, you created the same four sub-OUs:

- `Users`
- `Computers`
- `Servers`
- `Groups`

Repeat this process for each region:

1. Right-click the regional OU (example: `USA`)
2. Select:

   **New → Organizational Unit**

3. Create these OUs (one at a time):
   - `Users`
   - `Computers`
   - `Servers`
   - `Groups`

✅ Result (example for USA):  
USA  
├── Users  
├── Computers  
├── Servers  
└── Groups  


---

## Step 4 — Create Groups in Each Region

Within the **Groups** OU for each region (USA/Europe/Asia), you created:

1. **IT** (Security Group)
2. **DL-ITAdmins** (Distribution Group)

### 4A — Create the IT Security Group

For each region:

1. Expand:

   `Region → Groups`  
   Example: `USA → Groups`

2. Right-click **Groups**
3. Select:

   **New → Group**

4. Configure:
   - **Group name:** `IT`
   - **Group scope:** Global
   - **Group type:** Security

5. Click **OK**

### 4B — Create the Distribution Group (DL-ITAdmins)

Still inside the same `Groups` OU:

1. Right-click **Groups**
2. Select:

   **New → Group**

3. Configure:
   - **Group name:** `DL-ITAdmins`
   - **Group scope:** Global
   - **Group type:** Distribution

4. Click **OK**

✅ Example result for USA:  

USA  
└── Groups  
├── IT (Security Group)  
└── DL-ITAdmins (Distribution Group)    


---

## Step 5 — Create a User in USA → Users

You created a test user under:

`USA → Users`

1. Expand:

   `USA → Users`

2. Right-click **Users**
3. Select:

   **New → User**

4. Enter user details:
   - **Name:** Sam Pak
   - **Username:** (example) `spak`

5. Set a password and finish the wizard

✅ Result:  
USA  
└── Users  
└── Sam Pak  
--  

## Step 6 — Add Sam Pak to the IT and DL-ITAdmin Groups

You assigned the user to both a security group and a distribution group.

1. In ADUC, locate the user:

   `USA → Users → Sam Pak`

2. Right-click **Sam Pak** → **Properties**
3. Click the **Member Of** tab
4. Click **Add**
5. Add these groups:
   - `IT`
   - `DL-ITAdmin` (or `DL-ITAdmins`, depending on your exact name)

6. Click **Apply → OK**

✅ Outcome:
- Sam Pak is now a member of the **IT Security Group** (permissions/access)
- Sam Pak is also on the **DL-ITAdmin(s) Distribution Group** (email list)

---

## Step 7 — Create a New User by Copying an Existing User

Active Directory allows administrators to quickly create new users by **copying an existing user account**. This automatically inherits many properties such as **group memberships**, which significantly speeds up account provisioning.

This method is commonly used in enterprise environments when creating users with similar roles.

### Copy the Existing User

1. Navigate to:
USA → Users

2. Locate the existing user: Sam PAk

3. Right-click **Sam Pak**

4. Select: Copy

5. Enter the New User Information

When the **Copy Object Wizard** appears, enter the new user details.

Example:  
First Name: Tom  
Last Name: Brady  
User logon name: tombrady  

6. Click **Next**.

7. Set Password

Set an initial password for the new user and choose the appropriate options:

Typical lab settings:

- User must change password at next logon (optional)
- Password never expires (optional for lab)

8. Click **Finish**.  
Result  

A new user account is created:  
USA  
└── Users  
├── Sam Pak  
└── Tom Brady  


Because the account was copied from **Sam Pak**, the new user **Tom Brady automatically inherited the same group memberships**.

Example inherited groups:  
IT  
DL-ITAdmins  


---

### Verify Group Membership

To confirm the copied permissions:

1. Right-click **Tom Brady**
2. Select **Properties**
3. Open the **Member Of** tab

You should see: 
IT  
DL-ITAdmins  


---

## Why This Is Useful

Copying users is a common administrative practice because it:

- Reduces manual configuration
- Ensures consistent permissions
- Speeds up onboarding of employees with similar roles

Example real-world scenario:  
New IT employee joins team  
↓  
Copy existing IT user account  
↓  
Update name, username, password  
↓  
User automatically receives correct permissions  

