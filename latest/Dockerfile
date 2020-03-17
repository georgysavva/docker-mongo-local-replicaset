FROM mongo:latest

VOLUME /data
EXPOSE 27017 27018 27019

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]