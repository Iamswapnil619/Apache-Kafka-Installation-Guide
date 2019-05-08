# Apache-Kafka-Installation-Guide


Apache kafka mirrir site to install : https://www.apache.org/dyn/closer.cgi?path=/kafka/2.2.0/kafka_2.11-2.2.0.tgz

Apache kafka version : 2.2.0

This tutorial assumes you are starting fresh and have no existing Kafka or ZooKeeper data. Since Kafka console scripts are different for Unix-based and Windows platforms, on Windows platforms use bin\windows\ instead of bin/, and change the script extension to .bat. 

Step 1: Download the code
  - Download the 2.2.0 release and un-tar it. 
  - Go to C:\kafka\kafka_2.11-2.2.0\kafka_2.11-2.2.0\config folder
  - open server.properties file and change the log.dirs paramter to local path created. 
		e.g. # A comma separated list of directories under which to store log files
             log.dirs=C:\kafka\kafka-logs
			 
  - open zookeeper.properties and change the dataDir parameter to local path created. 
		e.g # the directory where the snapshot is stored.
             dataDir=C:\kafka\zookeeper-logs

Step 2: Start the server

  - Start the zookeper Server. ( Kafka uses ZooKeeper so you need to first start a ZooKeeper server if you don't already have one) 
	C:\kafka\kafka_2.11-2.2.0\kafka_2.11-2.2.0\bin\windows>zookeeper-server-start.bat config\zookeeper.properties

  - Now start the Kafka server:
	C:\kafka\kafka_2.11-2.2.0\kafka_2.11-2.2.0\bin\windows>kafka-server-start.bat config\server.properties

Step 3: Create a topic
  
  - Let's create a topic named "items-topic" with a single partition and only one replica
    
	C:\kafka\kafka_2.11-2.2.0\kafka_2.11-2.2.0\bin\windows>kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic items-topic
	
  - We can now see that topic if we run the list topic command:
    
Step 4: Send some messages
  
  - Kafka comes with a command line client that will take input from a file or from standard input and send it out as messages to the Kafka cluster. By   default, each line will be sent as a separate message.
  
  -	Run the producer and then type a few messages into the console to send to the server.
    C:\kafka\kafka_2.11-2.2.0\kafka_2.11-2.2.0\bin\windows>kafka-console-producer.bat --broker-list localhost:9092 --topic items-topic

Step 5: Start a consumer
  - Kafka also has a command line consumer that will dump out messages to standard output.
    C:\kafka\kafka_2.11-2.2.0\kafka_2.11-2.2.0\bin\windows>kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic items-topic --from-beginning

 
If you have each of the above commands running in a different terminal then you should now be able to type messages into the producer terminal and see them appear in the consumer terminal. 
