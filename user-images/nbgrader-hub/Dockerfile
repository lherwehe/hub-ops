# Install nbgrader and extensions on top of earthlab python env
FROM earthlab/earth-analytics-python-env:d53d66c

# Setup nbgitpuller to sync files from course repo to hub
RUN conda install -c conda-forge nbgitpuller \
    # abc-classroom for github classroom management
    abc-classroom>0.1.5 \
    && jupyter serverextension enable --py nbgitpuller --sys-prefix

# Setup nbzip - this allows students to download files from the hub
RUN pip install git+https://github.com/ryanlovett/jupyter-tree-download.git

# install jupyterhub from conda-forge and update jupyter_console
RUN conda install -c conda-forge jupyterhub \
    && pip uninstall --yes jupyter-console \
    && conda install -c conda-forge jupyter_console=6.0.0

# Setup nbgrader + extensions
RUN jupyter nbextension install --sys-prefix --py nbgrader --overwrite \
    && jupyter nbextension enable --sys-prefix --py nbgrader \
    && jupyter serverextension enable --sys-prefix --py nbgrader

# Install zip to support the download tool
USER root
RUN apt-get update && apt-get -y install  \
    # install open ssh to generate keys
    && apt-get -y install openssh-client
      
# For downgrade of nbconvert and traitlets following nbgrader setup.py file
RUN conda install -c conda-forge nbconvert==5.6.1 \
    traitlets==4.3.3
