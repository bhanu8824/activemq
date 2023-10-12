FROM ubuntu:22.04

ENV ACTIVEMQ_CONFIG_DIR /opt/activemq/conf.tmp
ENV ACTIVEMQ_DATA_DIR /data/activemq

# Update distro and install some packages
# Update the package list and install necessary packages
RUN apt-get update && \
    apt-get install --no-install-recommends -y python3 openjdk-11-jdk python3-pip vim curl supervisor logrotate locales && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install wheel and stompy using pip3
RUN pip3 install wheel stomp.py

# Lauch app install
COPY assets/setup/ /app/setup/
RUN chmod +x /app/setup/install && \
     /app/setup/install


# Copy the app setting
COPY assets/entrypoint /app/
COPY assets/run.sh /app/run.sh
RUN chmod +x /app/run.sh

# Expose all port
EXPOSE 8161
EXPOSE 61616
EXPOSE 5672
EXPOSE 61613
EXPOSE 1883
EXPOSE 61614

# Expose some folders
VOLUME ["/data/activemq"]
VOLUME ["/var/log/activemq"]
VOLUME ["/opt/activemq/conf"]

WORKDIR /opt/activemq

CMD ["/app/run.sh"]
