# linux-permissions-security

Linux file permissions and ownership project demonstrating access control and the principle of least # Linux Permissions Security Project

## Project Overview

In this project, I reviewed files and directories on a Linux system to identify inappropriate access permissions. I reviewed and changed file and directory ownership and modified permissions based on the principle of least privilege. This helped ensure that users and groups only had the access necessary to perform their roles.

## Scenario

After reviewing files and directories on a Linux system, I discovered that some had excessive or incorrect permissions. In this scenario, I needed to remove or modify permissions to ensure that users and groups only had the access necessary for their roles. These changes were made according to the principle of least privilege.

## Skills Demonstrated

- Used `ls -la` to review files, directories, hidden files, and their permissions.
- Interpreted Linux read (`r`), write (`w`), and execute (`x`) permissions for users, groups, and others.
- Used numeric and symbolic `chmod` commands to modify file and directory permissions.
- Used `chown` to change file ownership and group assignments.
- Identified excessive or incorrect permissions that could create security risks.
- Applied the principle of least privilege to restrict unnecessary access.

### 1. Excessive File Permissions

The original file was owned by `analyst` and assigned to the `staff` group, with read and write permissions granted to the owner, group, and other users.

`-rw-rw-rw- 1 analyst staff 2048 customer_data.txt`

These permissions provided more access than necessary. I changed the group from `staff` to `security`, limited the security group to read-only access, and removed all permissions from other users to follow the principle of least privilege.

```bash
chown analyst:security customer_data.txt
chmod 640 customer_data.txt
```
After remediation, the permissions were:

`-rw-r----- 1 analyst security 2048 customer_data.txt`

### 2. Excessive Script Permissions

The security script had incorrect ownership and allowed the owner, group, and other users to read, write, and execute the file.

`-rwxrwxrwx 1 guest users 4096 security_scan.sh`

I changed the owner to `analyst` and the group to `security`. I then granted the analyst read, write, and execute permissions, limited the security group to read and execute permissions, and removed all permissions from other users. This reduced unnecessary access and followed the principle of least privilege.

```bash
chown analyst:security security_scan.sh
chmod 750 security_scan.sh
```

After remediation, the permissions were:

`-rwxr-x--- 1 analyst security 4096 security_scan.sh`

### 3. Correctly Secured Sensitive File

The sensitive file already had appropriate permissions:

`-rw------- 1 analyst security 1024 credentials.txt`

Only the owner had read and write access, while the group and other users had no permissions. I did not use `chmod` or `chown` because the ownership and permissions already met the security requirements. Making unnecessary changes could alter an already secure configuration.

### 4. Secure Directory Permissions

The directory already had appropriate permissions:

`drwxr-x--- 2 analyst security 4096 .security`

The existing permissions matched the required security permissions. The owner had read, write, and execute permissions, the security group had read and execute permissions, and other users had no access.

For a directory, the execute (`x`) permission allows an authorized user to traverse the directory and access items within it. Since the existing ownership and permissions already met the security requirements, no remediation was necessary.

## Security Relevance

The principle of least privilege helps protect a system by giving users only the permissions necessary to perform their jobs. If a user account is compromised, limiting its permissions can also limit what an attacker is able to access, modify, or execute. Properly managing Linux permissions and ownership reduces unnecessary access to sensitive files and directories.

## Commands Used

- `ls -la` — Displayed files and directories, including hidden files, along with detailed permission and ownership information.
- `chmod 640 <file>` — Set the owner to read/write, the group to read-only, and other users to no access.
- `chmod 750 <file>` — Set the owner to read/write/execute, the group to read/execute, and other users to no access.
- `chmod g+w <file>` — Added write permission for the group.
- `chmod g-w <file>` — Removed write permission from the group.
- `chmod o-rwx <file>` — Removed all permissions from other users.
- `chown <user>:<group> <file>` — Changed the owner and group assigned to a file.

## Disclaimer

This project was completed as an educational cybersecurity exercise. The scenario, users, groups, files, and system data are simulated and do not represent a real production environment.