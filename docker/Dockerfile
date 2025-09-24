# Start with BioSim base image.
ARG BASE_IMAGE=latest
FROM ghcr.io/ccpbiosim/jupyterhub-base:$BASE_IMAGE

LABEL maintainer="James Gebbie-Rayet <james.gebbie@stfc.ac.uk>"
LABEL org.opencontainers.image.source=https://github.com/ccpbiosim/equilibration-workshop
LABEL org.opencontainers.image.description="A container environment for the ccpbiosim workshop on Equilibration."
LABEL org.opencontainers.image.licenses=MIT

# Switch to jovyan user.
USER $NB_USER
WORKDIR $HOME

# Install workshop deps
RUN mamba install matplotlib numpy ipywidgets -y
RUN pip install mdtraj

COPY --chown=1000:100 . .
RUN rm -rf AUTHORS LICENSE README.md docker .git .github && \
    mv equilT.png equilt.png

# Copy lab workspace
COPY --chown=1000:100 docker/default-37a8.jupyterlab-workspace /home/jovyan/.jupyter/lab/workspaces/default-37a8.jupyterlab-workspace

# UNCOMMENT THIS LINE FOR REMOTE DEPLOYMENT
COPY docker/jupyter_notebook_config.py /etc/jupyter/

# Always finish with non-root user as a precaution.
USER $NB_USER
