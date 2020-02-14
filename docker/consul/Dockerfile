# Base Image
FROM    alpine:3.7

# Set consul version and directory
ENV     CONSUL_DIR=/usr/src/consul
ENV     CONSUL_VERSION=1.7.0

# Create a directory and install dependencies
RUN     mkdir -p ${CONSUL_DIR} \
        && apk --no-cache add unzip bash curl wget ca-certificates

# Download and set a consul
RUN     wget --quiet \
        --output-document=/tmp/consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip  \
        && unzip /tmp/consul.zip -d ${CONSUL_DIR} \
        && rm -f /tmp/consul.zip \
        && chmod +x ${CONSUL_DIR}/consul \
        && ln -s ${CONSUL_DIR}/consul /usr/bin

# Add the config file
ADD     ./config/consul-config.json ${CONSUL_DIR}/config/config.json

# Expose ports
EXPOSE 8300 8400 8500 8600

# RUN Consul
ENTRYPOINT [ "consul" ]