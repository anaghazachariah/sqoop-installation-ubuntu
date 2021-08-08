
Prerequisite
*************

sudo apt update 
sudo apt install openjdk-8-jdk -y                          
java -version                                              
sudo apt install openssh-server openssh-client -y
sudo adduser hdoop
#the above command creates a new user.

su - hdoop
#The above command will change the user.Thhe command will ask password,use the password which you given during user creation

ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
ssh localhost
--------------------------------------------------------------------------------------------------------------------------------------------------
Installing Hadoop
*******************

wget https://archive.apache.org/dist/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz       
tar xzf hadoop-3.2.1.tar.gz


Editng 6 important files
=================================


1st file
===========================



#open file using following command
sudo nano .bashrc

#here you might face issue saying hdoop is not sudo user ,if this issue comes then(FOLLOWING 2 COMMANDS ARE NEEDED ONLY IF YOU ARE GETTING ERROR)
su - aman
sudo adduser hdoop sudo


#Add below lines in this file
export HADOOP_HOME=/home/hdoop/hadoop-3.2.1
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS"-Djava.library.path=$HADOOP_HOME/lib/nativ"



#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section



#type following command in terminal
source ~/.bashrc

2nd File
============================
#open file using following command
sudo nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh


#Add below line in this file in the end
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64


#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section

3rd File
===============================
#open file using following command
sudo nano $HADOOP_HOME/etc/hadoop/core-site.xml


#Add below lines in this file(between "<configuration>" and "<"/configuration>")
   <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/hdoop/tmpdata</value>
        <description>A base for other temporary directories.</description>
    </property>
    <property>
        <name>fs.default.name</name>
        <value>hdfs://localhost:9000</value>
        <description>The name of the default file system></description>
    </property>

 
#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section   

4th File
====================================
#open file using following command
sudo nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml


#Add below lines in this file(between "<configuration>" and "<"/configuration>")
<property>
  <name>dfs.data.dir</name>
  <value>/home/hdoop/dfsdata/namenode</value>
</property>
<property>
  <name>dfs.data.dir</name>
  <value>/home/hdoop/dfsdata/datanode</value>
</property>
<property>
  <name>dfs.replication</name>
  <value>1</value>
</property>



#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section


5th File
================================================
#open file using following command
sudo nano $HADOOP_HOME/etc/hadoop/mapred-site.xml

#Add below lines in this file(between "<configuration>" and "<"/configuration>")
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>


#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section


6th File
==================================================
#open file using following command
sudo nano $HADOOP_HOME/etc/hadoop/yarn-site.xml

#Add below lines in this file(between "<configuration>" and "<"/configuration>")
<property>
  <name>yarn.nodemanager.aux-services</name>
  <value>mapreduce_shuffle</value>
</property>
<property>
  <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
  <value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>
<property>
  <name>yarn.resourcemanager.hostname</name>
  <value>127.0.0.1</value>
</property>
<property>
  <name>yarn.acl.enable</name>
  <value>0</value>
</property>
<property>
  <name>yarn.nodemanager.env-whitelist</name>
  <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PERPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
</property>


#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section

=================================
#type following commands in terminal


rm -r /home/hdoop/hdoop-3.2.1/share/hdoop/common/lib/avro-1.7.7.jar
cd ~
cd hdoop-3.2.1/share/hdoop/common/lib
wget https://repo1.maven.org/maven2/org/apache/avro/avro/1.8.1/avro-1.8.1.jar
cd ~


hdfs namenode -format
cd ~/hadoop-3.2.1/sbin/
./start-dfs.sh
./start-yarn.sh
jps

#if your hadoop installation is successful,once you run jps command your system will list components of hadoop(DataNode,ResourceManager,NodeManager,Jps,NameNode,SecondaryNameNode)

hadoop version #to check hadoop version
------------------------------------------------------------------------------------------------------------------------------------------------------------------

Installing SQOOP
********************

cd~
cd hdoop-3.2.1/sbin
./start-all.sh 
cd ~
wget http://archive.apache.org/dist/sqoop/1.4.7/sqoop-1.4.7.tar.gz
tar -xvf sqoop-1.4.7.tar.gz

#Editing file
===========================

#open file using following command
sudo nano .bashrc


#Add below lines in this file
export SQOOP_HOME=/home/hdoop/sqoop-1.4.7
export PATH=$PATH:$HADOOP_HOME/sbin:$SQOOP_HOME/bin


#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section



#type following command in terminal
source ~/.bashrc
===========================

#type following command in terminal

cd $SQOOP_HOME/conf
mv sqoop-env-template.sh sqoop-env.sh




#Editing file
===========================

#open file using following command
nano sqoop-env.sh


#Add below lines in this file
export HADOOP_COMMON_HOME=/home/hdoop/hadoop-3.2.1
export HADOOP_MAPRED_HOME=/home/hdoop/hadoop-3.2.1


#press 'ctrl+x' then 'y key' then 'enter key' to save and close the coding section

===========================

cd $SQOOP_HOME/lib
wget https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.21/mysql-connector-java-8.0.21.jar
cd $SQOOP_HOME
wget https://talend-update.talend.com/nexus/content/repositories/libraries/org/apache/sqoop/sqoop/1.4.7/sqoop-1.4.7.jar
cp sqoop-1.4.7.jar bin/
cd $SQOOP_HOME/lib
wget https://repo1.maven.org/maven2/commons-lang/commons-lang/2.6/commons-lang-2.6.jar

sqoop version #To check sqoop version
-----------------------------------------------------------------------------------------------------------------------------------------------------


