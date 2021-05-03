# kafka Fraud Detector system

### Purpose: 
Building A Streaming Fraud Detection System With Kafka + Python

### Design:

The generator will generate the fake transactions and send to the kakfa topic queueing.transactions using kakfaProducer API. The detector will detect the transactions greater than $900 as fake transactions or else legit transactions and stream the data to the kakfa topics - streaming.transactions.fraud and streming.transactions.legit using kafkaConsumer API. 

### Steps to execute

1. create a docker network (kafka-network1) for the containers to communicate

docker network create kafka-network1

2. create a container for kafka cluster in undetached mode:

docker-compose -f docker-compose.kafka.yml up
 
3. create a container for generator and detector application 

docker-compose -f docker-compose.yml up
 
4. To verify the queueing.transactions transactions:

docker-compose -f docker-compose.kafka.yml exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic queueing.transactions --from-beginning

5. To verify the streaming.transactions.legit transactions:

docker-compose -f docker-compose.kafka.yml exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic streaming.transactions.legit

6. To verify the streaming.transactions.fraud transactions:

docker-compose -f docker-compose.kafka.yml exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic streaming.transactions.fraud

### Output screenshots

From queueing.transactions topic

![img1](https://github.com/bsathyamur/kafka-fraudDetector/blob/main/queueing.transactions.png)

From streaming.transactions.legit topic

![img2](https://github.com/bsathyamur/kafka-fraudDetector/blob/main/legit.png)

From streaming.transactions.fraud topic

![img3](https://github.com/bsathyamur/kafka-fraudDetector/blob/main/fraud.png)
