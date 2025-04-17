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
d  