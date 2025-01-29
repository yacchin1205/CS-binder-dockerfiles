FROM quay.io/jupyter/datascience-notebook:lab-4.3.4

COPY --chown=$NB_UID:$NB_GID ./python/Rprofile $HOME/.Rprofile

# Workaround: Node.js is missing in the latest base image
USER root
RUN apt-get update \
    && apt-get install -y curl \
    && curl -fsSL https://deb.nodesource.com/setup_20.x | sudo bash - \
    && apt-get install -y nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
USER $NB_UID

# Installing CS-jupyterlab-grdm https://github.com/RCOSDP/CS-jupyterlab-grdm/
ENV grdm_jlab_release_tag=0.3.0 \
    grdm_jlab_release_url=https://github.com/RCOSDP/CS-jupyterlab-grdm/releases/download/0.3.0
ENV jupyter_resource_usage_branch=main \
    jupyter_resource_usage_url=https://github.com/RCOSDP/CS-jupyter-resource-usage
RUN pip3 install jupyterlab-language-pack-ja-JP \
    && pip3 install ${grdm_jlab_release_url}/rdm_binderhub_jlabextension-${grdm_jlab_release_tag}.tar.gz \
    && jupyter labextension enable rdm-binderhub-jlabextension \
    && jupyter server extension enable rdm_binderhub_jlabextension \
    && jupyter nbclassic-extension install --py rdm_binderhub_jlabextension --user \
    && jupyter nbclassic-extension enable --py rdm_binderhub_jlabextension --user \
    && pip3 install git+${jupyter_resource_usage_url}@${jupyter_resource_usage_branch} \
    && npm cache clean --force \
    && pip3 cache purge
