Role Name
=========

A very simple role to perform a rolling restart of a Kafka cluster that waits for the cluster to recover before restarting the next cluster node.

Requirements
------------

No special requirements for the Ansible node.
Nodes that this role is run against are expected to have the kafka-topics tool installed an run a kafka service.

Role Variables
--------------

| Variable Name         | Description                                                                                                               | Default Value   |
|:----------------------|:--------------------------------------------------------------------------------------------------------------------------|:----------------|
| ZOOKEEPER_CONNECT     | Not currently in use                                                                                                      | kafka-topics    |
| NUMBER_OF_RETRIES     | The number of times to check whether all under-replicated partitions have been fixed.                                     | 10              |
| DELAY_BETWEEN_RETRIES | Seconds to wait between retries.                                                                                          | 15              |
| KAFKA_SERVICE_NAME    | Name of the Kafka service to be restarted.                                                                                | confluent-kafka |
| KAFKA_TOPICS_COMMAND  | Name (and path if necessary) of the kafka-topics tool - this is mostly to distinguish between Apache and Confluent Kafka. | kafka-topics    |



Dependencies
------------

None.

Example Playbook
----------------

For this role to work properly, it is very important to include _serial: 1_ in your playbook. Otherwise it will not be a rolling restart, as multiple hosts will be restarted at the same time, potentially leading to downtime.

`- hosts: kafka
  serial: 1
  roles:
    - kafka-rolling-restart`

License
-------
Apache 2.0

