FROM jwilder/nginx-proxy
RUN { \
      echo 'server_tokens off;'; \
      echo 'client_max_body_size 100m;'; \
      echo 'real_ip_header X-Forwarded-For;'; \
    } > /etc/nginx/conf.d/my_proxy.conf