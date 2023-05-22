FROM nginx
COPY ./server/mini_server.c /home/mini_server.c
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
WORKDIR /home/
RUN apt-get update && apt-get install -y gcc spawn-fcgi libfcgi-dev && \
    apt-get clean && rm -rf /var/lib/apt/lists && \
    gcc -Wall -Wextra -Werror mini_server.c -lfcgi -o mini_server && \    
    chown -R nginx:nginx /etc/nginx/nginx.conf && \
    chown -R nginx:nginx /var/cache/nginx && \
    touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid && \
    chmod u-s /usr/bin/gpasswd && \
    chmod g-s /usr/bin/chage && \
    chmod u-s /bin/mount && \
    chmod g-s /sbin/unix_chkpwd && \
    chmod u-s /usr/bin/chfn && \
    chmod u-s /bin/umount && \
    chmod g-s /usr/bin/expiry && \
    chmod g-s /usr/bin/wall && \
    chmod u-s /usr/bin/passwd && \
    chmod u-s /usr/bin/chsh && \
    chmod u-s /usr/bin/newgrp && \
    chmod u-s /bin/su
# EXPOSE 81
USER nginx
HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1    
CMD spawn-fcgi -p 8080 ./mini_server && nginx -g "daemon off;"