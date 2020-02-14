FROM    nginx:1.17.8-alpine

# Set consul version and directory
ENV     CONSUL_DIR=/usr/src/consul
ENV     CONSUL_VERSION=1.7.0

ADD     ./consul-config/nginx.json  ${CONSUL_DIR}/service/nginx.json

RUN     mkdir -p ${CONSUL_DIR}/data

RUN     apk --no-cache add unzip bash curl wget ca-certificates \
        && wget --quiet \
        --output-document=/tmp/consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip  \
        && unzip /tmp/consul.zip -d ${CONSUL_DIR} \
        && rm -f /tmp/consul.zip \
        && chmod +x ${CONSUL_DIR}/consul \
        && ln -s ${CONSUL_DIR}/consul /usr/bin

#RUN     consul agent -join 172.77.0.2 -enable-local-script-checks -data-dir=${CONSUL_DIR} -config-dir=${CONSUL_DIR}/service/nginx.json
