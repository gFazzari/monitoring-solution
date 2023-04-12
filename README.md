# What is this repository for?

This project creates an instance of **EFK** via docker compose.  
It uses *Zeek* and *Suricata* to analyze local network traffic received from the linked network interfaces.  
There is a *Fluentd* instance able to capure logs and upload them to *Opensearch* and to a remote *S3* bucket.  
It's also possible to analyze logs through the cool *Opensearch-Dashboards* exposed on port 6321.

## Set up

- create the .env file according to env.template 
- launch docker compose up --profile on-prem
- get the elastic container id:
docker ps
- launch the following command to reset all passwords in the opensearch container:
~~~~
bin/elasticsearch-setup-passwords auto
~~~~
- copy the printed credentials and update the .env file
- launch the following command to set specific passwords, e.g.
~~~~
bin/elasticsearch-reset-password -u elastic -i
~~~~
## Launch and stop compose with Suricata and Zeek
~~~~
docker compose --profile on-prem up -d
docker compose --profile on-prem down
~~~~
## Suricata

Rules location in the suricata container:

~~~~
var/lib/suricata/rules/
~~~~

Crontab to logrotate suricata and update suricata rules
~~~~

HOME=%PATH_TO_PROJECT%
0 6 * * * docker exec suricata logrotate -f /etc/logrotate.d/suricata
0 8 * * * docker exec suricata sh /opt/update_suricata.sh
~~~~


## Zeek config

The configs are modified via entrypoint.sh script.  

~~~~
/usr/local/zeek/etc/zeekctl.cfg
~~~~

## Multiple interfaces

~~~~
docker compose -f docker-compose.yml -f add-network-docker-compose.yml --profile on-prem up -d
~~~~