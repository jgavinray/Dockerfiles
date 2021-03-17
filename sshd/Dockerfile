FROM ubuntu:latest
LABEL maintainer "J. Gavin Ray <git@jgavinray.com>"

ENV SSH_USER "jgavinray"
ENV GITHUB_USER "jgavinray"

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y openssh-server rsync tmux sudo vim\
 && mkdir /var/run/sshd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin no/' /etc/ssh/sshd_config \
 && sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config \
 && sed -ri 's/^#?PasswordAuthentication\s+.*/PasswordAuthentication no/' /etc/ssh/sshd_config

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

EXPOSE 22

ENTRYPOINT ["entrypoint.sh"]
CMD ["/usr/sbin/sshd", "-D"]
