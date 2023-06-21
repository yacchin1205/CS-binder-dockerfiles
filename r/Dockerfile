FROM rocker/binder:4.1.2

# Installing CS-jupyterlab-grdm https://github.com/RCOSDP/CS-jupyterlab-grdm/
ENV grdm_jlab_release_tag=0.2.0.test3 \
    grdm_jlab_release_url=https://github.com/yacchin1205/CS-jupyterlab-grdm/releases/download/0.2.0.test3
RUN pip3 install jupyterlab-language-pack-ja-JP \
    && pip3 install ${grdm_jlab_release_url}/rdm_binderhub_jlabextension-refs.tags.${grdm_jlab_release_tag}.tar.gz \
    && jupyter labextension install ${grdm_jlab_release_url}/rdm-binderhub-jlabextension-refs.tags.${grdm_jlab_release_tag}.tgz \
    && jupyter labextension enable rdm-binderhub-jlabextension \
    && jupyter server extension enable rdm_binderhub_jlabextension \
    && jupyter nbclassic-extension install --py rdm_binderhub_jlabextension --user \
    && jupyter nbclassic-extension enable --py rdm_binderhub_jlabextension --user \
    && jlpm cache clean \
    && npm cache clean --force \
    && pip3 cache purge

# Installing CS-jupyterlab-grdm https://github.com/RCOSDP/CS-rstudio-grdm/
RUN R -e 'devtools::install_github("yacchin1205/CS-rstudio-grdm", ref = "fix/default-storage-provider", type = "source")';
