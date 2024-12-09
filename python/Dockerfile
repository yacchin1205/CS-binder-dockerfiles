FROM quay.io/jupyter/scipy-notebook:lab-4.2.6

COPY --chown=$NB_UID:$NB_GID ./python/Rprofile $HOME/.Rprofile

# Installing CS-jupyterlab-grdm https://github.com/RCOSDP/CS-jupyterlab-grdm/
ENV grdm_jlab_release_tag=0.3.0 \
    grdm_jlab_release_url=https://github.com/RCOSDP/CS-jupyterlab-grdm/releases/download/0.3.0
ENV jupyter_resource_usage_branch=main \
    jupyter_resource_usage_url=https://github.com/RCOSDP/CS-jupyter-resource-usage
RUN pip3 install jupyterlab-language-pack-ja-JP \
    && pip3 install ${grdm_jlab_release_url}/rdm_binderhub_jlabextension-${grdm_jlab_release_tag}.tar.gz \
    && jupyter labextension install ${grdm_jlab_release_url}/rdm-binderhub-jlabextension-${grdm_jlab_release_tag}.tgz \
    && jupyter labextension enable rdm-binderhub-jlabextension \
    && jupyter server extension enable rdm_binderhub_jlabextension \
    && jupyter nbclassic-extension install --py rdm_binderhub_jlabextension --user \
    && jupyter nbclassic-extension enable --py rdm_binderhub_jlabextension --user \
    && pip3 install git+${jupyter_resource_usage_url}@${jupyter_resource_usage_branch} \
    && npm cache clean --force \
    && pip3 cache purge
