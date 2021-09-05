# Deploy Kubernetes Cluster and Kafka Server
## Usage

### Clone repository
git clone https://github.com/jonandez/vagrant.git


### Create environment 
Run Vagrantfile script

```
vagrant up
```

### Connect to the servers
```
vagrant ssh kafka
vagrant ssh kmaster
vagrant ssh kworker1

```

### Check Kafka Topics
#### List Topics:
--bootstrap-server=localhost:9092 --list

#### Watch topics messages
~/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic input --from-beginning
~/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic output --from-beginning

### Check metrics
#### Prometheus Dashboard
172.16.16.101:30000

#### Grafana Dashboard
172.16.16.101:32000
User: admin
Password: admin

Import Kuberntes Dashboard
Go to left menu and select + and Import
Import using Grafana input code: 8588
Select Prometheus and click Import

### Decode message
Connect to kmaster server
```
vagrant ssh kmaster

```

Execute app.py
```
sudo python3 /home/vagrant/app/kafka_apps/decode/decode.py

```