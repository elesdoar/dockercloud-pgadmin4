FROM python:3.6-alpine

# runtime dependencies
RUN set -ex \
	&& apk add --no-cache --virtual .pgadmin4-rundeps \
		bash \
		postgresql

ENV PGADMIN4_VERSION 4.10
ENV PGADMIN4_DOWNLOAD_URL https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v${PGADMIN4_VERSION}/pip/pgadmin4-${PGADMIN4_VERSION}-py2.py3-none-any.whl

# Metadata
LABEL org.label-schema.name="pgAdmin4" \
      org.label-schema.version="$PGADMIN4_VERSION" \
      org.label-schema.license="PostgreSQL" \
      org.label-schema.url="https://www.pgadmin.org" \
      org.label-schema.vcs-url="https://github.com/elesdoar/dockercloud-pgAdmin4"

RUN set -ex \
	&& apk add --no-cache --virtual .build-deps \
		build-base \
		gcc \
		musl-dev \
		postgresql-dev \
		libffi-dev \
		linux-headers \
	&& pip --no-cache-dir install \
		$PGADMIN4_DOWNLOAD_URL \
	&& apk del .build-deps

VOLUME /var/lib/pgadmin

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 5050
CMD ["pgadmin4"]
