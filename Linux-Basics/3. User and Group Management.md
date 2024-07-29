# User and Group Management Commands

## User Management

### `adduser` / `useradd`
Creates a new user.
```bash
adduser username
useradd username

# Example
sudo adduser newuser
# Follow prompts to set password and user information
```

### `passwd`
Changes a user's password.
```bash
passwd username

# Example
sudo passwd newuser
# Follow prompts to set the new password
```

### `deluser` / `userdel`
Deletes a user.
```bash
deluser username
userdel username

# Example
sudo deluser newuser
# Output:
# Removing user `newuser' ...
```

### `usermod`
Modifies a user account.
```bash
usermod [options] username

# Example
sudo usermod -aG sudo newuser
# Adds newuser to the sudo group
```

### `id`
Displays user ID and group ID information.
```bash
id username

# Example
id newuser
# Output:
# uid=1001(newuser) gid=1001(newuser) groups=1001(newuser),27(sudo)
```

### `who`
Shows who is logged on.
```bash
who

# Example
who
# Output:
# user1   tty7         2024-07-27 09:32 (:0)
# user2   pts/1        2024-07-27 09:35 (192.168.1.2)
```

### `last`
Shows a list of last logged in users.
```bash
last

# Example
last
# Output:
# user1   pts/1        192.168.1.2     Mon Jul 26 09:35   still logged in
# user2   tty7         :0              Mon Jul 26 09:32   still logged in
```

## Group Management

### `addgroup` / `groupadd`
Creates a new group.
```bash
addgroup groupname
groupadd groupname

# Example
sudo addgroup newgroup
# Output:
# Adding group `newgroup' (GID 1002) ...
```

### `delgroup` / `groupdel`
Deletes a group.
```bash
delgroup groupname
groupdel groupname

# Example
sudo delgroup newgroup
# Output:
# Removing group `newgroup' ...
```

### `groupmod`
Modifies a group.
```bash
groupmod [options] groupname

# Example
sudo groupmod -n newgroupname oldgroupname
# Renames oldgroupname to newgroupname
```

### `gpasswd`
Administers `/etc/group` and `/etc/gshadow`.
```bash
gpasswd [options] groupname

# Example
sudo gpasswd -a newuser newgroup
# Adds newuser to newgroup
```

### `groups`
Displays groups a user is in.
```bash
groups username

# Example
groups newuser
# Output:
# newuser : newuser sudo
```

## User and Group Information Files

### `/etc/passwd`
Contains user account information.

#### Format
```
username:x:UID:GID:full_name:home_directory:shell
```

#### Example
```
newuser:x:1001:1001::/home/newuser:/bin/bash
```

#### Components
- `username`: The user's login name.
- `x`: Placeholder for the password (passwords are stored in `/etc/shadow`).
- `UID`: User ID number.
- `GID`: Group ID number.
- `full_name`: The user's full name or comment field.
- `home_directory`: The path to the user's home directory.
- `shell`: The path to the user's login shell.

### `/etc/shadow`
Contains secure user account information.

#### Format
```
username:password:last_change:min:max:warn:inactive:expire:reserved
```

#### Example
```
newuser:$6$randomhash:18295:0:99999:7:::
```

#### Components
- `username`: The user's login name.
- `password`: The user's encrypted password.
- `last_change`: The date of the last password change (in days since Jan 1, 1970).
- `min`: The minimum number of days between password changes.
- `max`: The maximum number of days the password is valid.
- `warn`: The number of days before password expiration that the user is warned.
- `inactive`: The number of days after password expiration that the account is disabled.
- `expire`: The date when the account expires (in days since Jan 1, 1970).
- `reserved`: Reserved field for future use.

### `/etc/group`
Contains group information.

#### Format
```
groupname:x:GID:user_list
```

#### Example
```
newgroup:x:1002:
```

#### Components
- `groupname`: The name of the group.
- `x`: Placeholder for the password (if any).
- `GID`: Group ID number.
- `user_list`: A comma-separated list of users that are members of the group.

### `/etc/gshadow`
Contains secure group account information.

#### Format
```
groupname:password:admin_list:user_list
```

#### Example
```
newgroup:::newuser
```

#### Components
- `groupname`: The name of the group.
- `password`: The group's encrypted password (if any).
- `admin_list`: A comma-separated list of group administrators.
- `user_list`: A comma-separated list of group members.

