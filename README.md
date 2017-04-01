Solution for problem given @ http://acesinc.net/introducing-a-streaming-json-data-generator/

Steps to run in local Start ZooKeeper & Kafka Broker on port 9092 (You can have as many brokers as you wish)

Create Kafka Topic for the below json-producer
./kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic jackieChanCommand

Download the JAR and run 
java -jar json-data-generator-1.1.0.jar jackieChanSimConfig.json

package using SBT and run the JAR using spark-submit
./spark-submit --master local[*] \
--driver-java-options "-Dlog4j.configuration=file:/home/srini/Srini_Programs/spark-2.1.0-bin-hadoop2.7/conf/log4j_sampleLogDriver.properties" \
--conf "spark.executor.extraJavaOptions=-Dlog4j.configuration=file::/home/srini/Srini_Programs/spark-2.1.0-bin-hadoop2.7/conf/log4j_sampleLogExecutor.properties" \
--packages org.apache.spark:spark-streaming-kafka_2.11:1.6.3 \
--class KafkaClient ../../../Srini_Scala_Programs/jackiechan-problem_2.11-1.0.jar localhost:9092 jackieChanCommand
