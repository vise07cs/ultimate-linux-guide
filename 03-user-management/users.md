# to create a new user
useradd username
to verify is user is created --> vim /etc/passwd  or cat /etc/passwd--> check in the bottom 
ls /home --> empty
useradd doesnt create a home directory for the user
# to create a password 
passwd username
to verify if password is created -->  cat /etc/shadow -->  (will show encypted password)

can we decrypt the passwoed ? what if the user forgets his pw ??  vvi interview qs --> answer is NO , you cannot decrypt and if someone forgets the password then there is no way you can restore the password . 

# to create a user with home directory 
adduser username  (enter all the details )
ls /home  --> user created in home directory 

# to switch user
su - username

# to check which user you are currently
whoami

# lets try to delete sbin directory as new-user 
rm -rf /sbin
rm: cannot remove '/sbin': Permission denied  --> this happened due to the usem mgmt by Linux 
(but we could have allowed it by using file permissions)

if we ran the above comand(rm -rf /sbin) as root user all the foldr would have been deleted and the system would have curroupted

# to logout as the user
logout

# Imp interview Qs
1) what is the difference between adduser and useradd
useradd is a quick way of creating user , it doesnt create home directory and also doesnt takes any  information for creating user.
useradd is very important when you are writing scripts 

adduser created a home directory for the user and while creating the user it also takes a lot of information about the user

2) can we decrypt the passwoed ? what if the user forgets his pw ??  vvi interview qs --> answer is NO , you cannot decrypt and if someone forgets the password then there is no way you can restore the password .
hence while creating a user , the password must be saved somewhere by the Admin

# Now lets learn about groups:
Why do we need groups ?
suppose you have 500 users in org (200 Dev , 100 DevOps ,200 from management)
Now to add or remove permission you would have to deal with 100s or even 1000s of files which is not possible  
As the no. of users will increase , it will become more and more complex to manegae users
Insted you should create  a group and users will be added to that group and you can modify the changes at group level
dev-->
DevOps-->

# How to create a group
groupadd devops
to verify -->  cat /etc/group  (check in the bottom)
 
 # to add a user to the group
  usermod -aG devops vsingh
  to verify -->  cat /etc/group  you will get output like --> (devops:x:1001:vsingh) (This means vsingh user is the part of DevOps group)

  # ssh 
  Every Linux server has sshd
  to connect to a linux machine you need a ssh client which has ssh 
  popular ssh clients (windows --> gitbash , mac --> terminal (iterm2) , )