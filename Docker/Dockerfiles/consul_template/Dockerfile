FROM debian:jessie

ENV TEMPLATE=/usr/local/src/consul_template.ctmpl
ENV NGINX_CONTAINERNAME=nginx

COPY nginx_template.ctmpl ${TEMPLATE}


# Install consul template
RUN \
  apt-get update && \
  apt-get install -y curl unzip && \
  curl -L https://releases.hashicorp.com/consul-template/0.15.0/consul-template_0.15.0_linux_amd64.zip > /tmp/consul_template.zip && \
  unzip /tmp/consul_template.zip -d /usr/local/bin && \
  chmod +x /usr/local/bin/consul-template && \
  mkdir -p /etc/nginx/conf.d

# Install Docker
RUN \
  apt-get install -y apt-transport-https ca-certificates && \
  apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D && \
  echo 'deb https://apt.dockerproject.org/repo debian-jessie main' > /etc/apt/sources.list.d/docker.list && \
  apt-get update && \
  apt-get install -y docker-engine

CMD CONSUL_TEMPLATE_LOG=debug \
    consul-template \
    -consul=${CONSUl_HOST} \
    -template "${TEMPLATE}:/etc/nginx/conf.d/default.conf:docker exec ${NGINX_CONTAINERNAME} kill -HUP 1"
