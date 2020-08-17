# Kafka Streams Demo

This is a small demo using Kafka streams based on [official docs](https://kafka.apache.org/26/documentation/streams/tutorial)

This is a very simple Kafka to Kafka sink which consumes data from one existing Kafka topic and push into another topic. 

## How to Run

### Run Kafka
In order to run it locally, we need to have a up running Kafka. 

Follow the [step 1 and step 2](https://kafka.apache.org/quickstart) to download and spin up the kafka broker locally.

### Create Topics
Then create 2 topics defined in this app by running the following command inside of the kafka folder:

```bash
# create input topic
$ bin/kafka-topics.sh --create \                                  
    --bootstrap-server localhost:9092 \
    --replication-factor 1 \
    --partitions 1 \
    --topic streams-input

# create output topic
$ bin/kafka-topics.sh --create \                                  
    --bootstrap-server localhost:9092 \
    --replication-factor 1 \
    --partitions 1 \
    --topic streams-output
```  

### Build & Run App

Run the following command line using Maven:

```bash
$ mvn clean package

$ mvn exec:java -Dexec.mainClass=myapps.Pipe
```

### Test via Producer and Consumer

Open a terminal and head to the Kafka folder. Run the console producer client to write a few events into the input topic.

```bash
bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic streams-input
```

Open another terminal session and run the console consumer client to read the events from the output topic

```bash
$ bin/kafka-console-consumer.sh --topic streams-output --bootstrap-server localhost:9092
```