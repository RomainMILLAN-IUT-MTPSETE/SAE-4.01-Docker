RUN apt-get updage && apt-get upgrade

RUN apt-get install --no-install-recommends -y --no-install-recommends  \
    python3 python3-pip wget gcc postgresql-15-postgis-3 postgresql-15-postgis-3-scripts \
    libnewlib-arm-none-eabi avr-libc git libpq-dev libssl-dev libc6 gdal-bin

RUN apt-get install postgis

RUN psql -h localhost -p 5432 -U postgres
RUN CREATE EXTENSION postgis;


