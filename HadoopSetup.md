#Setup hadoop single cluster on your Ubuntu

Download the required file from these links:  
[Hadoop 1.2.1](https://archive.apache.org/dist/hadoop/core/hadoop-1.2.1/hadoop-1.2.1.tar.gz)  
[Sample Files](https://drive.google.com/file/d/0B3ao8wGOP6diZXRnTE5YVEx6UXc/view?usp=sharing)

1.Create a new user "hadoop" and add it to the sudoers group.  
Login in to your normal user profile and enter the following commands:
```
sudo su -
sudo adduser hadoop
sudo adduser hadoop sudo
```
##All the steps below should be done after logging into your newly created "hadoop" user.

2.Extract the Hadoop file into a folder "hadoop" in your /home directory
```
tar -xf hadoop-1.2.1.tar.gz -C /home/hadoop
```
Now extract the sample files into the directory created inside "hadoop" file in your home directory.
It should be /home/hadoop/hadoop-1.2.1/[sample files here]
```
unzip mapreduce_workshop.zip -d /home/hadoop/hadoop-1.2.1
```
3.Now you need to modify files in the hadoop-1.2.1/conf
Edit the following files using any editor you like and save them.  
(Taken from [Single node setup guide](http://hadoop.apache.org/docs/r1.2.1/single_node_setup.html))  
conf/core-site.xml:
```
<configuration>
     <property>
         <name>fs.default.name</name>
         <value>hdfs://localhost:9000</value>
     </property>
</configuration>
```

conf/hdfs-site.xml:
```
<configuration>
     <property>
         <name>dfs.replication</name>
         <value>1</value>
     </property>
</configuration>
```

conf/mapred-site.xml:
```
<configuration>
     <property>
         <name>mapred.job.tracker</name>
         <value>localhost:9001</value>
     </property>
</configuration>
```
If you get any read/write permission error, change the permission using chmod
Try:(from /hadoop-1.2.1/)
```
chmod a=rxw conf or chmod 777 conf
```
gives all users(a) read (r), write (w) and execute (x) permission for conf folder
check using
```
ls -l
```

4.Login to your new hadoop user account and install SSH  
   1. Run the following commands in a terminal
   2. sudo apt-get install ssh
   3. sudo apt-get install rsync
   4. Setup passphraseless ssh (means running the command “ssh localhost” must not prompt for a password). Run the following commands in a terminal (one after the other)
   5. ```ssh-keygen   -t    dsa   -P  ""   -f   ~/.ssh/id_dsa```
   6. ```cat    ~/.ssh/id_dsa.pub    >>     ~/.ssh/authorized_keys```
Test if you installed it properly by typing:  
```
jps
```
You should see  
```
jps xxxx
```
xxxx - any processes ID  
Now type:
```
ssh localhost
```
This should now open a new prompt.