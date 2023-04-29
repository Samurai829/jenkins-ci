FROM centos:7

MAINTAINER samurai829

RUN yum -y install openssh-server
 
RUN yum install -y passwd
 
RUN useradd remote_user && \
    echo "remote_user:1234" | chpasswd && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh

WORKDIR /home/remote_user/

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

# Aqui creamos una maquina remota con CentOS, donde instalamos 
# OpenSSH agregamos un Usuario y indicamos una contraseña
# Se creo un directorio .ssh debajo del directorio Home
# ademas de darle permisos 700 al directorio
# por ultimo agregamos key ssh al directorio

RUN chown remote_user:remote_user -R /home/remote_user/.ssh/

RUN /usr/bin/ssh-keygen -A
# Aqui damos mas permisos a la carpeta "remote_user" y 
# al archivo en la carpeta

#RUN /usr/sbin/sshd-keygen > /dev/null 22>&1

CMD ["/usr/sbin/sshd", "-D"]