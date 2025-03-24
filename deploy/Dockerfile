FROM oven/bun:latest

WORKDIR /app

RUN apt-get update && \
    apt-get install -y nginx supervisor

RUN bun install cheerio pino pino-pretty

COPY . .

COPY supervisord.conf /app/supervisord.conf

RUN addgroup --system nginx && \
    adduser --system --no-create-home --disabled-login --ingroup nginx nginx

RUN apt-get clean && rm -rf /var/lib/apt/lists/*


COPY deploy/dist /usr/share/nginx/html/

COPY deploy/nginx.conf /etc/nginx/nginx.conf

COPY deploy/start.sh /app/start.sh

RUN chmod +x /app/start.sh
RUN chmod +x /app/supervisord.conf


EXPOSE 80

CMD ["supervisord", "-c", "/app/supervisord.conf"]
