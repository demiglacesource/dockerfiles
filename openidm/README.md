openidm
=========

Dockerfile for OpenIDM to build a docker container.

Run
-----

    $ git clone https://github.com/demiglacesource/dockerfiles && cd dockerfiles/openidm
    $ docker build -t openidm .
    $ docker run -d -p 8080:8080 openidm

Sharing Directories using volumes
-----------------------------------

    $ wget http://download.forgerock.org/downloads/openidm/snapshot/openidm-3.2.0-SNAPSHOT.zip
    $ unzip openidm-3.2.0-SNAPSHOT.zip -d /opt
    $ docker run -d -p 8080:8080 -v /opt/openidm/conf:/opt/openidm/conf:rw -v /opt/openidm/logs:/opt/openidm/logs:rw  openidm

Link
------

* https://forgerock.org/openidm
* http://openidm.forgerock.org/docs.html

