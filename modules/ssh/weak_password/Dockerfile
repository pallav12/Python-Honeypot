# using phusion/baseimage as base image
FROM phusion/baseimage:0.9.19

# update and install openssh + python
RUN apt-get update && apt-get install -y openssh-server

# create credential
RUN echo {username}:{password} | /usr/sbin/chpasswd

# config ssh
RUN sed -i 's/#Port 22/Port 22/g' /etc/ssh/sshd_config
RUN sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/g' /etc/ssh/sshd_config

# run ssh-keygen non-interactive
RUN ssh-keygen -k -f id_rsa -t rsa -N '' -f /root/.ssh/id_rsa >/dev/null && service ssh restart

# start the service + wait for container
ENTRYPOINT service ssh restart && tail
