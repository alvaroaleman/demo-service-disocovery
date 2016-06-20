FROM nginx:latest


COPY proxy_params /etc/nginx/proxy_params

# Log to stdout instead of files
# Also we want the notice level to get info about config reloads
RUN \
  sed -i 's/^error_log.*/error_log \/dev\/stderr notice;/g' /etc/nginx/nginx.conf
