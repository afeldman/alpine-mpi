FROM afeldman/alpine-openmpi:onbuild

ARG REGISTRY_ADDR=localhost
ARG REGISTRY_PORT=5000
ARG IMAGE_NAME=mpi
ARG SSH_PORT=2222

ENV REGISTRY_ADDR=${REGISTRY_ADDR}
ENV REGISTRY_PORT=${REGISTRY_PORT}
ENV IMAGE_NAME=${IMAGE_NAME}
ENV SSH_PORT=${SSH_PORT}

# # ------------------------------------------------------------
# # Build MPI project
# # ------------------------------------------------------------

# Put all build steps and additional package installation here

# Note: the current directory is ${WORKDIR:=/project}, which is
# also the default directory where ${USER:=mpi} will SSH login to

# Copy the content of `project` directory in the host machine to 
# the current working directory in this Docker image
COPY project/ .

# Normal build command
RUN mpicc -o mpi_hello_world mpi_hello_world.c
