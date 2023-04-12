FROM zeek/zeek:5.0.6

RUN apt-get update &&\
    apt-get install -y --no-install-recommends g++ cmake make libpcap-dev iproute2 nload htop ethtool

ENV PATH "/usr/local/zeek/bin:${PATH}"

RUN zkg autoconfig --force &&\
    zkg install --skiptests --force zeek/ncsa/bro-doctor &&\
    zkg install --skiptests --force mitre-attack/bzar && \
    zkg install --skiptests --force add-node-names

RUN cd /opt &&\
    git clone https://github.com/J-Gras/zeek-af_packet-plugin.git &&\
    cd zeek-af_packet-plugin &&\
    ./configure --with-latest-kernel && make && make install

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

WORKDIR /usr/local/zeek

CMD ["/entrypoint.sh"]