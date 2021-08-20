su - hdoop
wget https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
tar xzf apache-hive-3.1.2-bin.tar.gz





Edit .bashrc file
========================
sudo nano .bashrc




export HIVE_HOME= /home/hdoop/apache-hive-3.1.2-bin
export PATH=$PATH:$HIVE_HOME/bin
=================================



source ~/.bashrc




Edit hive-config.sh
====================================
sudo nano $HIVE_HOME/bin/hive-config.sh




export HADOOP_HOME=/home/hdoop/hadoop-3.2.1
===============================



hdfs dfs -mkdir /tmp
hdfs dfs -chmod g+w /tmp
hdfs dfs -mkdir -p /user/hive/warehouse
hdfs dfs -chmod g+w /user/hive/warehouse


Edit guava-19.0.jar
====================================
rm $HIVE_HOME/lib/guava-19.0.jar


cp $HADOOP_HOME/share/hadoop/hdfs/lib/guava-27.0-jre.jar $HIVE_HOME/lib/
===============================

chematool -initSchema -dbType derby
cp /home/hdoop/apache-hive-3.1.2-bin/lib/hive-common-3.1.2.jar /home/hdoop/sqoop-1.4.7/lib/hive-common-3.1.2.jar


#to  get hive prompt
hive

#to show databases
    show databses

#to use a database
    use zakku;

#to show tables in database
    show tables;

#to create table
    create table emp1(id int);