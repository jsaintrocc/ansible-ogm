carbon
======

Role which helps to manage Carbon installation. It uses `defaults` variables to
generate the main Carbon and storage schemas configuration files.


Example
-------

```
---

# Default installation
- hosts: myhost1
  roles:
    - carbon

# Custom config installation
- hosts: myhost2
  roles:
    - role: carbon
      carbon_config:
        cache:
          STORAGE_DIR: /var/lib/carbon/
          LOCAL_DATA_DIR: /var/lib/carbon/whisper/
          WHITELISTS_DIR: /var/lib/carbon/lists/
          CONF_DIR: /etc/carbon/
          LOG_DIR: /var/log/carbon/
          PID_DIR: /var/run/
          ENABLE_LOGROTATION: 'False'
          USER: carbon
          MAX_CACHE_SIZE: inf
          MAX_UPDATES_PER_SECOND: 500
          MAX_CREATES_PER_MINUTE: 50
          LINE_RECEIVER_INTERFACE: 0.0.0.0
          LINE_RECEIVER_PORT: 2003
          ENABLE_UDP_LISTENER: 'False'
          UDP_RECEIVER_INTERFACE: 0.0.0.0
          UDP_RECEIVER_PORT: 2003
          PICKLE_RECEIVER_INTERFACE: 0.0.0.0
          PICKLE_RECEIVER_PORT: 2004
          LOG_LISTENER_CONNECTIONS: 'True'
          USE_INSECURE_UNPICKLER: 'False'
          CACHE_QUERY_INTERFACE: 0.0.0.0
          CACHE_QUERY_PORT: 7002
          USE_FLOW_CONTROL: 'True'
          LOG_UPDATES: 'False'
          LOG_CACHE_HITS: 'False'
          LOG_CACHE_QUEUE_SORTS: 'True'
          CACHE_WRITE_STRATEGY: sorted
          WHISPER_AUTOFLUSH: 'False'
          WHISPER_FALLOCATE_CREATE: 'True'
        relay:
          LINE_RECEIVER_INTERFACE: 0.0.0.0
          LINE_RECEIVER_PORT: 2013
          PICKLE_RECEIVER_INTERFACE: 0.0.0.0
          PICKLE_RECEIVER_PORT: 2014
          LOG_LISTENER_CONNECTIONS: 'True'
          RELAY_METHOD: rules
          REPLICATION_FACTOR: 1
          DESTINATIONS: 127.0.0.1:2004
          MAX_DATAPOINTS_PER_MESSAGE: 500
          MAX_QUEUE_SIZE: 10000
          USE_FLOW_CONTROL: 'True'

      carbon_storage_schemas:
        # Store 10 seconds samples for 7 days
        carbon:
          pattern: ^carbon\.
          retentions: 10:7d
        default_1min_for_1day:
          pattern: .*
          retentions: 60s:1d
```


Role variables
--------------

List of variables used by the role:

```
# Default main configuration
carbon_config:
  cache:
    STORAGE_DIR: /var/lib/carbon/
    LOCAL_DATA_DIR: /var/lib/carbon/whisper/
    WHITELISTS_DIR: /var/lib/carbon/lists/
    CONF_DIR: /etc/carbon/
    LOG_DIR: /var/log/carbon/
    PID_DIR: /var/run/
    ENABLE_LOGROTATION: 'False'
    USER: carbon
    MAX_CACHE_SIZE: inf
    MAX_UPDATES_PER_SECOND: 500
    MAX_CREATES_PER_MINUTE: 50
    LINE_RECEIVER_INTERFACE: 0.0.0.0
    LINE_RECEIVER_PORT: 2003
    ENABLE_UDP_LISTENER: 'False'
    UDP_RECEIVER_INTERFACE: 0.0.0.0
    UDP_RECEIVER_PORT: 2003
    PICKLE_RECEIVER_INTERFACE: 0.0.0.0
    PICKLE_RECEIVER_PORT: 2004
    LOG_LISTENER_CONNECTIONS: 'True'
    USE_INSECURE_UNPICKLER: 'False'
    CACHE_QUERY_INTERFACE: 0.0.0.0
    CACHE_QUERY_PORT: 7002
    USE_FLOW_CONTROL: 'True'
    LOG_UPDATES: 'False'
    LOG_CACHE_HITS: 'False'
    LOG_CACHE_QUEUE_SORTS: 'True'
    CACHE_WRITE_STRATEGY: sorted
    WHISPER_AUTOFLUSH: 'False'
    WHISPER_FALLOCATE_CREATE: 'True'
#  relay:
#    LINE_RECEIVER_INTERFACE: 0.0.0.0
#    LINE_RECEIVER_PORT: 2013
#    PICKLE_RECEIVER_INTERFACE: 0.0.0.0
#    PICKLE_RECEIVER_PORT: 2014
#    LOG_LISTENER_CONNECTIONS: 'True'
#    RELAY_METHOD: rules
#    REPLICATION_FACTOR: 1
#    DESTINATIONS: 127.0.0.1:2004
#    MAX_DATAPOINTS_PER_MESSAGE: 500
#    MAX_QUEUE_SIZE: 10000
#    USE_FLOW_CONTROL: 'True'
#  aggregator:
#    LINE_RECEIVER_INTERFACE: 0.0.0.0
#    LINE_RECEIVER_PORT: 2023
#    PICKLE_RECEIVER_INTERFACE: 0.0.0.0
#    PICKLE_RECEIVER_PORT: 2024
#    LOG_LISTENER_CONNECTIONS: 'True'
#    FORWARD_ALL: 'True'
#    DESTINATIONS: 127.0.0.1:2004
#    REPLICATION_FACTOR: 1
#    MAX_QUEUE_SIZE: 10000
#    USE_FLOW_CONTROL: 'True'
#    MAX_DATAPOINTS_PER_MESSAGE: 500
#    MAX_AGGREGATION_INTERVALS: 5

# Default storage configuration
carbon_storage_schemas:
  carbon:
    pattern: ^carbon\.
    retentions: 60:90d
  default_1min_for_1day:
    pattern: .*
    retentions: 60s:1d
```


License
-------

MIT


Author
------

Jiri Tyr