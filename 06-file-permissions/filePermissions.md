
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

chmod o= helloWorld.sh

Now if we try to read the file as qe user --> it will throw an error
--> Permission denied



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


