RUN apt-get updage && apt-get upgrade

RUN apt-get install --no-install-recommends -y --no-install-recommends  \
    python3 python3-pip wget gcc postgresql-15-postgis-3 postgresql-15-postgis-3-scripts \
    libnewlib-arm-none-eabi avr-libc git libpq-dev libssl-dev libc6 gdal-bin

RUN apt-get install postgis

WORKDIR /
RUN touch index.html

RUN psql -h localhost -p 5432 -U postgres
RUN CREATE EXTENSION postgis;

#CREATE DATABASE SAE-401
RUN CREATE DATABASE SAE401;

#CREATE TABLE
RUN create table troncon_route(gid serial primary key,id_rte500 varchar(24),vocation varchar(80),nb_chausse varchar(80),nb_voies varchar(80),etat varchar(80),acces varchar(80),res_vert varchar(80),sens varchar(80),num_route varchar(24),res_europe varchar(200),longueur double precision,class_adm varchar(20),geom geometry(LineString, 4326));
RUN create table noeud_routier(gid serial primary key,id_rte500 varchar(24),nature varchar(80), insee_comm varchar(5), geom geometry(Point, 4326));
RUN create table noeud_commune(gid serial primary key,id_rte500 varchar(24),insee_comm varchar(5),nom_chf varchar(200),statut varchar(30),nom_comm varchar(100),superficie double precision,population double precision,id_nd_rte  varchar(24),geom geometry(Point, 4326));