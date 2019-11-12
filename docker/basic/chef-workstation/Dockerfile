FROM chef/chefdk

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
      apt-get install -y ssh vim iproute2 wget && \
      mkdir -p /root/.chef/cookbooks && \
      mkdir -p /root/.chef/data_bags && \
      echo "root:toor" | chpasswd && \
      sed -ri 's/^#?PasswordAuthentication\s+.*/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
      sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
      sed -ri 's/UsePAM\syes/#UsePAM yes/g' /etc/ssh/sshd_config && \
      service ssh start && \
      rm -rf /var/lib/apt/lists/*

COPY chef-workstation/run.sh /usr/local/bin/
COPY files/hello /root/.chef/cookbooks

CMD run.sh; /usr/sbin/sshd -D