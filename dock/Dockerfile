# Floreant POS Dockerfile
#
# https://github.com/genome21/Floreantpos-1
#

FROM centos:centos7
MAINTAINER Robert Wilkins III <thecainvestors@gmail.com>

TAG latest

# Install
RUN yum -y update; yum clean all
RUN yum -y install git; yum clean all
RUN yum -y epel-release; yum clean all
RUN yum -y install x11vnc xterm tigervnc-server xorg-x11-server-Xvfb xorg-x11-twm xorg-x11-font dejavu-sans-fonts dejavu-serif-fonts xdotool; yum clean all

# Add the xstartup file into the image
ADD ./xstartup /

RUN mkdir /.vnc
RUN x11vnc -storepasswd 123456 /.vnc/passwd
RUN \cp -f ./xstartup /.vnc/.
RUN chmod -v +x /.vnc/xstartup

EXPOSE 5901

CMD	["vncserver", "-fg" ]
# ENTRYPOINT ["vncserver", "-fg" ]

# Define working directory.
WORKDIR /usr/Downloads


# Clone the git repo to the docker container
RUN git clone git@github.com:genome21/floreantpos-1.git

# Run Floreant POS
ADD ./start-server.sh /start-server.sh
ADD ./floreantpos.bat /floreantpos.bat
RUN ./start-server.sh
RUN ./floreantpos.bat