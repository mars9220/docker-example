FROM ubuntu:18.04

# Ignore all interactive dialog during apt-get update
ENV DEBIAN_FRONTEND noninteractive

# RUN sed -i 's/archive.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list
RUN apt-get update && apt-get upgrade -y
RUN apt-get install build-essential libssl-dev libffi-dev python3-dev python3-pip curl sudo openssh-server vim htop screen reptyr git libproj-dev proj-data proj-bin libgeos-dev python3-tk -y

# Add all user into sudoers
RUN echo '%staff   ALL=(ALL:ALL) ALL' >> /etc/sudoers

# Nodejs install
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get update && apt-get upgrade -y
RUN apt-get install nodejs -y

# Python package install
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install shapely numpy scipy matplotlib --no-binary shapely; python3 -m pip --no-cache-dir install --upgrade jupyterlab ipympl pysmo.aimbat obspy rf Cartopy seaborn pylint flake8 yapf 

# Jupyter Lab interactive plot
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && jupyter labextension install jupyter-matplotlib --no-build
RUN jupyter lab build

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN mkdir /var/run/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# Clear login message for sftp login and add ls color
RUN echo 'alias ls="ls --color"' > /etc/bash.bashrc

# Start ssh service
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
