FROM centos:centos7

SHELL ["/bin/bash", "-c"]
User root

RUN yum install -y epel-release
RUN yum install -y supervisor
RUN yum install -y openssh-server
RUN yum install -y git
RUN yum install -y python36 python36-pip

COPY id_rsa /etc/ssh/ssh_host_rsa_key
RUN chmod 700 /etc/ssh/ssh_host_rsa_key
COPY id_rsa /root/.ssh/id_rsa
RUN chmod 700 /root/.ssh/id_rsa
COPY id_rsa.pub /root/.ssh/id_rsa.pub
RUN ssh-keyscan -H github.com >> /root/.ssh/known_hosts
RUN git clone git@github.com:teruuuuuu/kabuthon.git
RUN mv kabuthon /opt/
RUN cd /opt/kabuthon
RUN pip3 install --upgrade pip
RUN pip3 install -r /opt/kabuthon/requirements.txt
COPY .env /opt/kabuthon/kabuthon/
COPY brand_list.txt /opt/kabuthon/

RUN useradd rundeck
User rundeck
COPY id_rsa /home/rundeck/.ssh/id_rsa
COPY id_rsa.pub /home/rundeck/.ssh/id_rsa.pub
COPY authorized_keys /home/rundeck/.ssh/authorized_keys

User root

COPY supervisord.conf /etc/supervisord.conf
RUN chown -R rundeck:rundeck /opt/kabuthon/
CMD ["/usr/bin/supervisord"]


