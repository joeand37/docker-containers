FROM phusion/baseimage:0.9.16
MAINTAINER Zuhkov <zuhkov@gmail.com>

ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
	
EXPOSE 8080

VOLUME ["/config"]

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0xcbcb082a1bb943db && \
    echo "deb http://mariadb.mirror.iweb.com/repo/5.5/ubuntu `lsb_release -cs` main" \
    > /etc/apt/sources.list.d/mariadb.list

### Install packages and clean up in one command to reduce build size
RUN apt-get update

#RUN apt-get install -y --no-install-recommends mariadb-server
RUN apt-get install -y --no-install-recommends mariadb-server

RUN useradd myusertest && \
	chown -R myusertest:myusertest /var/log/mysql* && \
	chmod 777 /var/log/mysql* && \
	chmod -s /var/log/mysql*

# Execute these commands bellow to build and run docker container
	# docker build -t guacamole_bug .; docker stop guacamole_bug; rm -rf /your-config-location/; docker rm guacamole_bug; docker run -d -p 9001:8080 -v /your-config-location:/config --name guacamole_bug guacamole_bug
# Execute this command bellow to going on the container
	# docker exec -it guacamole_bug bash
# You can see the user "myusertest" have full rights on /var/log/mysql
	# ls -l /var/log | grep mysql
# Try create a file inside ; you will see "Permission denied"
	# su myusertest -s /bin/bash -c "touch /var/log/mysql/testcreatingfile"
# Try create a similar directory
	# mkdir /var/log/mysql2
	# chown myusertest:myusertest /var/log/mysql2
	# chmod 777 /var/log/mysql2
	# ls -l /var/log | grep mysql2
# Try create a file inside the similar directory ; you will the file is created
	# su myusertest -s /bin/bash -c "touch /var/log/mysql2/testcreatingfile"
