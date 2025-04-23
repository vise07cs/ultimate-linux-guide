
1st lets create 2 users 
adduser developer 
adduser qe
cat /etc/passwd


su - developer 
cd /tmp
vi helloWorld.sh
   --> 
      #!/bin/bash
      echo "Hello World"
Now switch as qe user and try to :
1) read file --> works fine
2) update file (using vi )--> throws an error

This shows Linux automatically implements permission at some extent 

we can even deny the read access to qe user : 
as developer user

chmod o= helloWorld.sh  (will revoke all permissions for others)
chmod go= filename  (will revoke all permissons for others as well as the group)



Now if we try to read the file as qe user --> it will throw an error
--> Permission denied

(However therse are not the best practices to deal with permissons , we can use numbered permission system as well)



---------------------------------------------------------------------------
mkdir folder1
touch file1

ls -ltr


drwxrwxr-x 2 developer developer 4096 Apr 22 12:46 folder1    (directory)
-rw-rw-r-- 1 developer developer    0 Apr 22 12:46 file1      (file)

-rw-rw---- 1 developer developer   31 Apr 22 12:19 helloWorld.sh (file)





# the 1st character represents if its a file or a directory 
In the above ex folder1 is  a directory (d)

if its not a directory , you will se - 
In the above ex file1 is  not a directory (-)

After the 1st character there are 9 different characters
All the 9 character can be split into 3 sets 
drwxrwxr-x
d | rwx | rwx | r-x


The 1st set represents the permission of the user   (user --> The one who created the file (From above example developer ))
The  2nd set represents the permission of the group  (group --> The group user belongs to  (ex: if Developer user belongs to Dev group ) )
The 3rd set represents the permission of others   (other linux users who are not the part of group (Ex : qe user is not the part of dev group))



Lest consider helloworld.sh file:     -rw-rw---- 1 developer developer   31 Apr 22 12:19 helloWorld.sh (file)
 -rw-rw----
-| rw- | rw- | ---

r-> read
w-> write or updating the file
x -> execute or executing the script
-  -> permission is missing 


our helloworld.sh file says ,
 -rw-rw---- 

 -| rw- | rw- | ---


 user has : rw-
read access (r)
write access (w)
but doesnt have execuatble access (-)


group the user belongs to has :  rw-
read access (r)
write access (w)
but doesnt have execuatble access (-)


other users: ---
no read access (we removed read access )
no write access
no executable access

 -----------------------------------------------------------------------------------

whoami
developer

 ./helloWorld.sh    (executing the shell script)
 Permission denied

 su - root
chmod u=rwx helloWorld.sh   (u=user , got r,w,x permissions)

su - developer 
./helloWorld.sh
output=Hello World


 su - root
chmod o=rwx helloWorld.sh

now other users can also read , write , execute the files 
(however , editing the file via vi/vim may still not be allowed for other users , this is due to linux /tmp directory level permission(internally dealt by linux ) . Hence we can verify the above operations in other location like home directory . It will work just fine there .  )

----------------------------------------------------------------------------------------------------

# File Permissions using number system
(4+2+1=7)
r--> 4
w-->2
x -->1

   user  | group | others
- |r w x | r w x | r w x 
   4 2 1 | 4 2 1 | 4 2 1  
 chmod 777 means you are giving all permission(r,w,x) to everyone 
 
 Ex : create a test file with read access only to user , group and others

  chmod 444 filename


Ex : create a test file with read,write,execute  access  to user , group and others
   chmod 777 filename


Ex : create a test file with read  access  to user only
chmod 400 filename

Ex : create a test file with read  access, write access   to user , group and others

chmod 666 filename

Ex : create a test file with read  access, write access   to user , group only 

chmod 660


The same rule applies to directory level too 

hence there are 2 ways using which you can manage the file permissions in Linux


chmod ---> u=rwx,g=rwx,o=rwx filename
chmod ---> chmod 777 filename


-----------------------------------------------------
# chown 
to change the ownership of the file or folder


drwxrwxr-x 2 developer developer 4096 Apr 22 12:46 folder1    (directory)

owner of the folder1 directory is developer 
The group which Developer belongs to is developer 


To change the ownership change to root user
chown qe:qe folder1 


owner changed to qe 

ls -ltr
drwxrwxr-x 2 qe qe 4096 Apr 22 12:46 folder1    (directory)


# what if there is  a permission on folder and file inside it as well and they have different sets of permissions which permission will apply in that case ?
(important interview question)

Similar concept as bank and locker . You can access locker only if you have access to the bank.  (bank=folder , locker= file ) 

in such cases  Folder permission will superimpose file permission
This means the folder level permissions  will get more priority 



