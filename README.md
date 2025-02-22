# Kafka_learn

# Apache Kafka Commands for Windows

## 1. **Setup & Installation**
### Download and Extract Kafka
1. Download Kafka from the official website: [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads)
2. Extract the downloaded file to a preferred location (e.g., `C:\kafka`).

### Configure Environment Variables (Optional)
- Add Kafka's `bin/windows` directory to the `PATH` variable for easier access to commands.

### Start Zookeeper (Required for Kafka)
Kafka requires Zookeeper for managing metadata. Start it using:
```sh
bin\windows\zookeeper-server-start.bat config\zookeeper.properties
```

### Start Kafka Broker
Once Zookeeper is running, start the Kafka broker:
```sh
bin\windows\kafka-server-start.bat config\server.properties
```

---

## 2. **Kafka Topic Management**

### Create a Topic
```sh
bin\windows\kafka-topics.bat --create --topic myTopic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```
- `--topic myTopic`: Specifies the topic name.
- `--partitions 1`: Number of partitions (adjust as needed).
- `--replication-factor 1`: Number of replicas (use `1` for a single-node setup).

### List All Topics
```sh
bin\windows\kafka-topics.bat --list --bootstrap-server localhost:9092
```

### Describe a Topic
```sh
bin\windows\kafka-topics.bat --describe --topic myTopic --bootstrap-server localhost:9092
```

### Delete a Topic
```sh
bin\windows\kafka-topics.bat --delete --topic myTopic --bootstrap-server localhost:9092
```

---

## 3. **Kafka Producer & Consumer**

### Start a Producer (Send Messages to Kafka)
```sh
bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic myTopic
```
- Start typing messages and press **Enter** to send them.

### Start a Consumer (Read Messages from Kafka)
```sh
bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic myTopic --from-beginning
```
- `--from-beginning`: Reads all messages from the beginning.

---

## 4. **Handling External Files (Sending Data to Kafka)**

### Send a Text File to Kafka
```sh
type C:\Users\malay\Desktop\data.txt | bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic myTopic
```

### Send CSV Data (PowerShell)
```powershell
Get-Content C:\Users\malay\Desktop\data.csv | bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic myTopic
```

---

## 5. **Consumer Group Management**

### List Consumer Groups
```sh
bin\windows\kafka-consumer-groups.bat --bootstrap-server localhost:9092 --list
```

### Describe a Consumer Group
```sh
bin\windows\kafka-consumer-groups.bat --bootstrap-server localhost:9092 --describe --group myGroup
```

### Reset Consumer Group Offset
```sh
bin\windows\kafka-consumer-groups.bat --bootstrap-server localhost:9092 --group myGroup --reset-offsets --to-earliest --execute
```

---

## 6. **Kafka Broker & Zookeeper Management**

### Stop Zookeeper
```sh
bin\windows\zookeeper-server-stop.bat
```

### Stop Kafka Broker
```sh
bin\windows\kafka-server-stop.bat
```

---

## 7. **Kafka in KRaft Mode (Without Zookeeper)**
Kafka introduced **KRaft Mode** (Kafka Raft) as a replacement for Zookeeper, improving scalability and reducing dependencies.

### Format Storage Directory (First Time Only)
```sh
bin\windows\kafka-storage.bat format -t <UUID> -c config\kraft\server.properties
```
- Replace `<UUID>` with a unique identifier (generate using `bin\windows\kafka-storage.bat random-uuid`).

### Start Kafka in KRaft Mode
```sh
bin\windows\kafka-server-start.bat config\kraft\server.properties
```

### Create a Topic in KRaft Mode
```sh
bin\windows\kafka-topics.bat --create --topic myTopic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

### List Topics in KRaft Mode
```sh
bin\windows\kafka-topics.bat --list --bootstrap-server localhost:9092
```

### Describe a Topic in KRaft Mode
```sh
bin\windows\kafka-topics.bat --describe --topic myTopic --bootstrap-server localhost:9092
```

### Stop Kafka in KRaft Mode
```sh
bin\windows\kafka-server-stop.bat
```

---

## 8. **Troubleshooting & Logs**

### Check Broker Logs
```sh
type logs\kafka-server.log
```

### Check Consumer & Producer Logs
```sh
type logs\consumer.log
type logs\producer.log
```

### Verify Kafka Server is Running
```sh
bin\windows\kafka-broker-api-versions.bat --bootstrap-server localhost:9092
```

---

## 9. **Useful Commands Summary**
| Command | Description |
|---------|-------------|
| `kafka-topics.bat --list` | List all topics |
| `kafka-topics.bat --describe --topic myTopic` | Get topic details |
| `kafka-console-producer.bat --broker-list localhost:9092 --topic myTopic` | Start a producer |
| `kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic myTopic --from-beginning` | Start a consumer |
| `kafka-consumer-groups.bat --list` | List consumer groups |
| `kafka-consumer-groups.bat --describe --group myGroup` | Describe a consumer group |
| `zookeeper-server-start.bat config\zookeeper.properties` | Start Zookeeper |
| `kafka-server-start.bat config\server.properties` | Start Kafka broker |
| `kafka-storage.bat format -t <UUID> -c config\kraft\server.properties` | Format Kafka storage for KRaft mode |
| `kafka-server-start.bat config\kraft\server.properties` | Start Kafka in KRaft mode |

This document provides all the essential Kafka commands needed to set up, manage, and troubleshoot Kafka on Windows, including KRaft mode.

