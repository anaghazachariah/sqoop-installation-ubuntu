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
