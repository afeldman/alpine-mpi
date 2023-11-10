FROM alpine:edge

LABEL org.opencontainers.image.authors="anton.feldmann@gmail.com"
LABEL version="1.0"
LABEL description=" build mpi server in a docker image file with \
alpine linux for a small head"

ARG REQUIRE="sudo build-base openmpi openmpi-dev openmpi-doc openssh"
RUN apk update && apk upgrade \
      && apk add --no-cache ${REQUIRE}
RUN apk update && apk add ca-certificates && update-ca-certificates && apk add openssl

#### TEST openmpi INSTALLATION ####
RUN mkdir /tmp/mpi_test
WORKDIR /tmp/mpi_test
COPY mpi_test .
RUN sh test.sh
RUN rm -rf /tmp/mpi_test

#### CLEAN UP ####
WORKDIR /
RUN rm -rf /tmp/*


#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
RUN adduser -D ${USER} \
      && echo "${USER}   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
RUN adduser -D ${USER} \
      && echo "${USER}   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

ENV USER_HOME /home/${USER}
RUN chown -R ${USER}:${USER} ${USER_HOME}

#### CREATE WORKING DIRECTORY FOR USER ####
ARG WORKDIR=/project
ENV WORKDIR ${WORKDIR}
RUN mkdir ${WORKDIR}
RUN chown -R ${USER}:${USER} ${WORKDIR}

WORKDIR ${WORKDIR}
USER ${USER}

CMD ["/bin/bash"]