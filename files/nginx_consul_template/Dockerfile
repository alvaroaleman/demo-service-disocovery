FROM nginx:latest

ENV TEMPLATE=/etc/consul_template.ctmpl

COPY proxy_params /etc/nginx/proxy_params
COPY nginx_template.ctmpl ${TEMPLATE}

RUN \
  apt-get update && \
  apt-get install -y curl unzip && \
  curl -L https://releases.hashicorp.com/consul-template/0.15.0/consul-template_0.15.0_linux_amd64.zip > /tmp/consul_template.zip && \
  unzip /tmp/consul_template.zip -d /usr/local/bin && \
  chmod +x /usr/local/bin/consul-template

CMD service nginx start & \
    CONSUL_TEMPLATE_LOG=debug \
    consul-template \
    -consul=${CONSUl_HOST} \
    -template "${TEMPLATE}:/etc/nginx/conf.d/default.conf:service nginx reload"
