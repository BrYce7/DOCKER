FROM postgres:9.5

COPY ./init-db.sql /docker-entrypoint-initdb.d/

VOLUME  ["/var/lib/postgresql/data"]
