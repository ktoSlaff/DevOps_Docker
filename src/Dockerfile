FROM nginx
COPY ./server/mini_server.c /home/mini_server.c
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
WORKDIR /home/
RUN apt-get update && apt-get install -y gcc spawn-fcgi libfcgi-dev && \
    apt-get clean && rm -rf /var/lib/apt/lists && \
    gcc -Wall -Wextra -Werror mini_server.c -lfcgi -o mini_server &&
CMD spawn-fcgi -p 8080 ./mini_server && nginx -g "daemon off;"