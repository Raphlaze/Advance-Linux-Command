# Advance-Linux-Command
## File Permissions and Access Rights
In the beginning of this project i learnt to understand how to manage file permissions and ownership in Linux. The knowledge empowers me to control access to files and directories, ensuring security and integrity of my system.

## Numeric Representation of Permissions
In Linux, permissions are represented using numeric values. Each permissions which are (no permission, read, write, and execute) are assigned a numeric value:
* no permissions = 0
* read = 4
* write = 2 
* execute = 1

This values are combined to represent the permissions for each user class.

### Permissions Represented by 7
* 4 (read) + 2 (write) + 1 (execute) = 7
* Symbolic: rwx
* Meaning: Read, Write and execute permissions are granted

### Permissions Represented by 5
* 4 (read) + 1 (execute) = 5
* Symbolic: r-x
* Meaning: Read and execute permissions are granted but write permission is not.

### Permissions Represented by 6
* 4 (read) + 2 (write) = 6
* symbolic: rw-
Meaning: Read and Write permissions are granted but execute permission is not.

### Understanding User Classes From a Permissions Perspective
User classes are categories of users that Linux recognizes when deciding who can do what with a file. There are three main classes namely:

* Owner: The person who created the file. Often referred to as the 'user'.
* Group: A collection of users who share certain permissions for the file.
* Others: Anyone else who has access to the computer but doesn't fall into the first two categories.

### The Role of Hyphens (-) in Permission Representation
A hyphen doesn't actually represent a user class. Instead its used in the symbolic representation of permissions to show the absence of a permission.
E.g I got into my Linux Terminal and ran the following command below:

**ls -latr**
The img below shows the outcome of the command

![ls-latr](./Img/ls-latr.png)

* In the output above, you will notice that some of the first character  can be a  **- or d**  **d** means its a directory while **-** means its a file.

* The next three characters (**rwx**) shows the permissions for the owner, **r** stands for read, **w** for write and **x** for execute.

* If a permission is not granted, you will see a **-** in its place (e.g., r-x means read and execute permissions are granted but write is not)

* The hyphen seperates, owner, group, and others.
* The following three characters after the owner's permissions represent the group's permission, using the same r, w, and x notation.
* The last three characters shows the permission for others.

The order the user class is represented is as follows:
* The first hyphen **"-"** is the **user**
* The second hyphen **"-"** is the **group**
* The Third hyphen **"-"** is the **others**

## File Permission Commands
To manage file permissions and ownership, Linux provides several commands:

### Chmod Command
The 'Chmod' command allows you to modify file permissions. you can use both symbolic and numeric representations to assign permissions to the user, group and other.
The example i did was to create an empty file using the 'touch' command, the command ran is shown below:

**touch script.sh**

Then to check the permission of the file, i used the command below:

**ls -latr script.sh**

below shows the output of the permission granted.

![touch-script](./Img/touch-script.png)

I noticed the above output does not have execute permissions, to update the permission so that all user classes will have execute permissions the command below is ran.

**chmod +x script.sh**

The above uses +x option to grant execute to the file 'script.sh'. The +x option adds the execute permission to the existing permissions for all the user classes.
To check again same command is ran below:

**ls -latr script.sh**

Output image of the permissions granted is shown below:

![chmod+x](./Img/chmod-script.png)

The same command can be executed to achieve the same result using the numbers approach.
Command is shown below:

**chmod 755 script.sh**

What makes it 755 is because:
* (4+2+1)= 7 for the user (read, write and execute).
* (4+1)= 5 for the group (read and execute)
* (4+1)= 5 for others (read and execute)

Output of the command is shown in image below:

![chmod755](./Img/chmod-num.png)

Another example i carried out was with 'chmod 777, giving all user classes permissions to read, write and execute. Command used is shown below:

**chmod 777 nano_file**

To check the output, command used was:

**ls -latr nano_file**

The output of the command ran, shows the user classes permission all in read, write and execute granted. Img is shown below:

![chmod777](./Img/chmod777.png)

### Chown Command
The chown command allows you to change the ownership of files, directories or symbolic links to a specified username or group.
For example changing from a server to another, example used is ran in the command below:

**chown raphlaze:developer nano_file**

checked the output with ls -latr command then i saw the new changes

## Superuser Privilledges
Its often necessary to become the superuser to perform important tasks in Linux. The command that gives us superuser priviledges is called '**sudo**'. To use i simply type "sudo" followed by the command i want to invoke.

An example is shown below using the command sudo:

**sudo i**

This is to switch to root user. Output image is shown below:

![sudo-i](./Img/sudo-i.png)

Then type exit, to leave the shell.

## User Management on Linux
As a devops engineer, i am also to do system administration which involves managing different users on the servers. Tasks like how to create a new user or group, modifying their permissions and updates passwords and similar tasks.

### Creating a User
To create a new user on ubuntu server, you can use the 'adduser' command.
For example,
i tried creating a new user with a name Raphlaze. command is shown below:

**sudo adduser johndoe**

running this command prompt me to enter and confirm a password for the new user. I was also asked to provide additional information. Once done the user account will be created and a home directory was automatically generated for the user.

The home directory represents a file system directory created in the name of the user. Such as '/home/johndoe'. This is where each user created on the server will store their respective data. Below is a image of the output.

![adduser](./Img/add-user.png)

### Granting Administrative Privileges
By default, newly created user accounts do not have administrative access to a user, but can be added to the sudo group.
Users in sudo group can run commands with administrative privileges. To add ***johndoe*** user to the sudo group, i ran the command below:

**sudo usermod -aG sudo johndoe**

* Usermod: This is a command that modifies user account properties.
* -aG: These are flags used with the usermod command
* -a stands for "append" and is used to add the user to  specific group(s) without removing them from other groups they may already belong to.
* G stands for "supplementary groups" and is followed by a comma-seperated list of groups. It specifies the groups to which the user shoud be added or modified.
* In a given command '-aG sudo' is used to add the user 'johndoe' to the **sudo** group.

### Switching User Accounts
To start using the system as another user, i will need to use the 'su' command to switch.
for example i would practice the tasks for me
1. Log out and in back as the newly created user
2. Navigate to the 'home/johndoe' directory to explore what has been created. using 'cd' command.

1. The following command below was used to switch users

**su raphlaze**

below is resulted image of its output:

![raphlaze](./Img/tasks1.png)

2. The command below was used to navigate the 'home/raphlaze' user directory, using the 'cd' command.

**cd raphlaze**

below is the resulted image of its output:

![taskcd](./Img/taskcd.png)

## Modifying User Accounts
### Changing User Password
To change the password for a user, the 'passwd' command followed by the username is used.
below is a task of the command i ran changing password for raphlaze user.

**sudo passwd raphlaze**

I was prompted to enter and confirm new password.
below is the output image of the command ran and password changed.

![passwd](./Img/change-usr-passwd.png)

### Creating a Group
To create a new group, i use the 'groupadd' command.
for example i created a group called "developers", the command i used is stated below:

**sudo groupadd developers**

Below is a image of the output to show work done.

![groupadd](./Img/groupadd.png)

### Adding Users to the Group
To add users to the group, i made use of 'usermod' command.
For example i added user raphlaze to the developers group using the command below:

**sudo usermod -aG developers raphlaze**

### Verifying Group Memberships
To confirm the group membership for a specific user, i use the 'id' command. For example to confirm the above command i wrote earlier for adding user raphlaze to the developers group. The command below was what i used to verify.

**id raphlaze**

The command displays information about the user 'raphlaze', including the groups they belong to, such as the "developers" that was just created.
The image below shows the information about the command used.

![id](./Img/id-raphlaze.png)

### Deleting a User 
To delete a user the command 'userdel' is used.
Below is an example of a command i used in deleting an already existing user.

**sudo userdel johndoe**

Below is an output image to show work done:

![userdel](./Img/userdel.png)

### Ensuring Proper Group Permissions
Groups in Linux are often used to manage permissions for files and directories. Ensuring that relevant files and directories have the appropriate group ownership and permissions. For example to grant the "developers" group ownership of a directory, the command below was used:

**sudo chown :developers**

And to grant read and write permissions to the group, the command below was used:

**sudo chown g+rw**

## Side Hustle Task 3
* Create a group on the server and name it 'devops'

Command below was used to create it followed by an image output:

**sudo groupadd devops**

![devops](./Img/group-devops.png)

* Create 5 users '["mary", "mohammed", "ravi", "tunji", "sofia"]' and ensure each user belong to the devops group.

Command used for creating user mary and image output are shown below:

**sudo adduser mary**

![mary](./Img/user-mary.png)

Command used for creating user mohammed and image output are shown below:

**sud adduser mohammed**

![mohammed](./Img/user-mohammed.png)

Command used for creating user ravi and image output are shown below:

**sudo adduser ravi**

![ravi](./Img/user-ravi.png)

Command used for creating user tunji and image output are shown below:

![tunji](./Img/user-tunji.png)

Command used for creating user sofia and image output are shown below:

**sudo adduser sofia**

![sofia](./Img/user-sofia.png)

* Create a folder for each user in the '/home' directory

The command used in creating Folders for the five users are seen below

**mkdir mary**

**mkdir mohammed**

**mkdir ravi**

**mkdir tunji**

**mkdir sofia**

The image below shows folders created for all five user folders created in the home directory

![dir](./Img/foldershome.png)

* Ensure that the group ownership of each created folder belongs to **"devops"**

The command used for ownership for mary to belong to devops group is seen below along side its image output.

**sudo usermod -aG devops mary**

![marydevops](./Img/marydevops.png)

The command used for ownership for mohammed to belong to devops group is seen below along side its image output.

**sudo usermod -aG devops mohammed**

![mohdevops](./Img/mohammedevops.png)

The command used for ownership for ravi to belong to devops group is seen below along side its image output.

**sudo usermod -aG devops ravi**

![ravidevops](./Img/ravidevops.png)

The command used for ownership for tunji to belong to devops group is seen below along side its image output.

**sudo usermod -aG devops tunji**

![tunjidevops](./Img/tunjidevops.png)

The command used for ownership for sofia to belong to devops group is seen below along side its image output.

**sudo usermod -aG devops sofia**

![sofiadev](./Img/sofiadevops.png).

This brings us to the end of this project called Advance Linux Command, thanks for your time.
