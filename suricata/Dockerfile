FROM jasonish/suricata:6.0

COPY update_suricata.sh /opt/update_suricata.sh

COPY suricata.logrotate /etc/logrotate.d/suricata

RUN chmod a+x /opt/update_suricata.sh

ENTRYPOINT ["/bin/sh", "-c", "/opt/update_suricata.sh ; /docker-entrypoint.sh"]