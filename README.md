# Altschool assignment on users, groups and permissions within the terminal in Linux operating system.

## A full detail on how to create user, group and give specific permissions to users/group using the visudo file within the terminal in Linux operating system.

This small project can give Linux enthusiasts a overview of how to create user/groups and also give permissions to a certain user/group to perform certain sudo operations without giving them full administrative priviledge. The commands here will be given based on the assumptions that the individual is logged in as a root user. In case you are not logged in as  a root user, the command "sudo su" can be used to switch to root user or start every command with the tag "sudo" to access administrative privilages. 

* Create a user
* Set an expiry date for user
* Prompt the user to change their password on login 
* Attach the user to a group
* Allow group users to be able to run only cat command on the /etc/ folder/files 
* Create a user without a home directory

# Create a user
To create a user, the command "useradd username" can be used. some common options as regard to useradd include;
1. -s => this specifies the shell required for the user
2. -g => specifies the group to which user will be assigned to
3. -e => used to set expiry date to user
4. -d => to create a home directory along with user etc

There are alot of other options regarding the "useradd" which I cannot go in details to. To assess the full description of "useradd" command and it's options, input the command "useradd -h" or "useradd --help" in your machine terminal. 

# Set an expiry date for user 
To set an expiry date for a user, the command "usermod --expiredate YYYY-MM-DD username" can be used. Replace `username` with the actual username of the user and `YYYY-MM-DD` with the desired expiration date of user. 


# Prompt the user to change their password on next login 
To promp a user to change their password on next login, we simply make the current password of the user to expire. In that case, when he/her log in next a prompt will come up to set a new password. The command line can be used to achieve this using the following step;
1. Open a Terminal
2. Use the "passwd -e YYYY-MM-DD username" command to set an expiration date for the user password. Replace `username` with the actual username of the user and `YYYY-MM-DD` with the desired password expiration date. 

# Attach the user to a group
To attach a specific user to a group, the command "usermode" can be used in the following steps; 
1. Open a Terminal
2. Use the "usermod -aG groupname username" command to assign a user to a specific group. Replace `username` with the actual username of the user and `groupname` with the name of the actual group assigned to. 

# Create a user without a home directory
The following step can be followed:
1. Open a Terminal
2. Input "useradd -M username". replace the 'username' with the desired name of user.  

# Allow group users to be able to run only cat command on the /etc/ folder/files 
input the line below in the "sudoers" file using the visudo command.

" %Altschool ALL=(ALL) /bin/cat /etc/* "

The breakdown of the line above is given as; 
'%Altschool': This specifies a group ('%' indicates a group) called `Altschool`.

"ALL=(ALL)": This part defines the scope of the command. The first `ALL` refers to any user the rule applies to. The second `(ALL)` refers to any target user they can run commands as (usually `root`).

"/bin/cat": This is the path to the command that users in the group `Altschool` are allowed to execute with `sudo`. In this case, it's the `cat` command.

"/etc/*": This specifies the path for files that the `cat` command can be used on. The `*` is a wildcard character that matches any file within the `/etc/` directory.

So, the line you provided allows users in the `Altschool` group to use the `sudo` command to run the `cat` command on any file within the `/etc/` directory as the root user. This can be useful for allowing members of the group to read configuration files in the `/etc/` directory without giving them full administrative privileges.

Always be cautious when modifying the `sudoers` file, as it controls access to sensitive system functions. Make sure to test thoroughly and understand the security implications of any changes you make.


