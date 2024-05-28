# syntax=docker/dockerfile:1
FROM fschmitt/clustered_network_pub:nest2_20

# make sure we have a CLI editor
RUN apt-get install -y vim nano

# install datalad in the conda env, hoping pip is more lightweight
RUN conda activate EI_clustered_network && pip install datalad

# --- required by binder ---
# https://mybinder.readthedocs.io/en/latest/tutorials/dockerfile.html

RUN python3 -m pip install --no-cache-dir notebook jupyterlab bash_kernel
RUN python -m bash_kernel.install

ARG NB_USER=jovyan
ARG NB_UID=1000
ENV USER ${NB_USER}
ENV NB_UID ${NB_UID}
ENV HOME /home/${NB_USER}

RUN adduser --disabled-password \
    --gecos "Default user" \
    --uid ${NB_UID} \
    ${NB_USER}

# Make sure the contents of our repo are in ${HOME}
COPY . ${HOME}
USER root
RUN chown -R ${NB_UID} ${HOME}
USER ${NB_USER}

# --- other tweaks on top ---

# the base docker image defines workdir in /app
# however, here we need (?) to run as user jovyan
# and some jupyter lab functionalities do not work when dropped into (root-owned?) /app
WORKDIR ${HOME}

# some tweaks from the base docker image need to be applied for the non-root user
# todo: possibly also library paths?

RUN conda init bash

# set git config
RUN git config --global user.name "Dr. Panik" && git config --global user.email "panik@example.com"
