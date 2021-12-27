# TODO
FROM postgres:11.6-alpine

COPY src/db/init-products-db.sh /docker-entrypoint-initdb.d/

ENV POSTGRES_PASSWORD=widgetario
# We use Postgres for the database, version 11.6 - it can use a minimal OS.

# There's an init script which populates the reference data that we need to include:
#  - src/db/init-products-db.sh

# Your base image should make it easy to run that script as part of the container startup.