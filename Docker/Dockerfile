FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

###################################### user #####################################

ENV SHELL=/bin/bash \
    USER=arg \
    UID=1000 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8

ENV HOME=/home/${USER}

RUN adduser --disabled-password \
    --gecos "Default user" \
    --uid ${UID} \
    ${USER} 

RUN echo "root:root" | chpasswd
RUN echo "${USER}:111111" | chpasswd

###################################### basic tools #####################################

RUN apt-get -o Acquire::ForceIPv4=true update && apt-get -yq dist-upgrade \
    && apt-get -o Acquire::ForceIPv4=true install -yq --no-install-recommends \
    locales \
    make \
    cmake \
    git \
    vim \
    gedit \
    wget \
    sudo \
    lsb-release \
    build-essential \
    net-tools \
    dirmngr \
    gnupg2 \
    mercurial \
    libopencv-dev \
    libcanberra-gtk-module \
    libcanberra-gtk3-module \
    libpcap-dev \
    python3-pip \
    python3-setuptools \
    python3-opencv \
    python3-numpy \
    python3-empy  \
    python3-lxml \
    python3-pymodbus \
    terminator \
    screen \
    nginx \
    openssh-server \
    libglfw3-dev \
    iputils-ping \
    libncurses5-dev \
    libgtk2.0-dev \
    libatk1.0-dev \
    libcairo2-dev \
    libx11-dev \
    libxpm-dev \
    libxt-dev \
    python3-dev \
    pybind11-dev \
    cmake \
    ctags \
    curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

##################################### PIP3 ######################################

RUN pip3 install --upgrade pip setuptools

RUN pip3 install \
    gdown \
    virtualenv \
    pytest \
    flask \
    flask-socketio \
    jupyter \
    virtualenv \
    nbdev \
    cmake \
    numpy \
    cython \
    pandas \
    image \
    Pillow \
    matplotlib \
    tensorflow \
    tensorboard \
    pygwidgets

# RUN pip install \
#     torch==1.10 \
#     torchvision==0.11.1 \
#     -f https://download.pytorch.org/whl/cu111/torch_stable.html

##################################### gym #####################################
RUN python3 -m pip install --upgrade pip
RUN pip3 install gymnasium[all]==0.26.2
RUN pip install gymnasium[box2d]
##################################### codon #####################################
RUN /bin/bash -c "$(curl -fsSL https://exaloop.io/install.sh)"
RUN export PATH=/home/${USER}/.codon/bin:$PATH

##################################### vim-python-ide ######################################
RUN git clone https://github.com/ARG-NCTU/vim-python-ide.git && \
    cd vim-python-ide && ./install.sh
####################################### pyivp ###########################################

RUN cd ${HOME} && git clone https://github.com/ARG-NCTU/pyivp.git \
    && cd pyivp \
    && make -f oop.Makefile
####################################### openai ###########################################
RUN pip install openai
####################################### pypy ###########################################
RUN apt update
RUN apt install --yes software-properties-common
RUN add-apt-repository --yes ppa:pypy/ppa
RUN apt install -y pypy3

####################################### nuitka ###########################################
RUN pip install nuitka
RUN apt install ccache

############################### pydot & grapghviz ###################################
RUN apt update
RUN apt install graphviz -y
RUN pip3 install pydot
##################################### meld #####################################
RUN apt-get install meld -y
################################# cloc ripgrep #####################################
RUN apt-get install cloc -y
RUN apt-get install ripgrep -y
##################################### setting #####################################

RUN chown -R ${USER}:${USER} ${HOME}/
RUN echo "${USER} ALL=(ALL)  NOPASSWD: ALL" > /etc/sudoers
RUN echo "export PATH=/home/${USER}/.codon/bin:$PATH" > /home/${USER}/.bashrc
    

USER ${USER}

WORKDIR ${HOME}
