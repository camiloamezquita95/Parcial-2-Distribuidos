FROM ubuntu:16.04
RUN apt-get update && apt-get install -y \
		ssh
RUN wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | apt-key add -
RUN apt-get update && apt-get install -y \
		postgresql postgresql-contrib 
RUN useradd -ms /bin/bash admin
COPY create_schema.sql /tmp/create_schema.sql
USER postgres
RUN service postgresql start && \
	sleep 40 &&\
	cat /tmp/create_schema.sql | psql
USER root
RUN rm /etc/postgresql/9.5/main/postgresql.conf
COPY postgresql.conf /etc/postgresql/9.5/main/postgresql.conf
RUN echo "host all all 172.17.0.1/16 trust" >> /etc/postgresql/9.5/main/pg_hba.conf
EXPOSE 5432
USER postgres
CMD ["/usr/lib/postgresql/9.5/bin/postgres", "-D", "/var/lib/postgresql/9.5/main", "-c", "config_file=/etc/postgresql/9.5/main/postgresql.conf"]
