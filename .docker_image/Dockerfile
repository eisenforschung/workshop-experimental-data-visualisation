ARG ROOT_CONTAINER=pyiron/md:latest
ARG BASE_CONTAINER=$ROOT_CONTAINER
FROM $BASE_CONTAINER

LABEL maintainer="Muhammad Hassani<hassani@mpie.de>"

USER $DOCKER_UID
WORKDIR $HOME
ARG PYTHON_VERSION=default

RUN rm -r ${HOME}/*
COPY environment.yml ${HOME}/
RUN conda install -y --quiet -c conda-forge mamba && \
    mamba env update -n base -f ${HOME}/environment.yml && \
    mamba clean --all -f -y

USER root
COPY start-singleuser.sh /usr/local/bin/
RUN fix-permissions /home/$DOCKER_USER && \
    fix-permissions $CONDA_DIR
# Switch back to pyiron to avoid accidental container runs as root
USER $DOCKER_UID

WORKDIR $HOME
