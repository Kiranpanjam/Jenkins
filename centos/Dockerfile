FROM centos

RUN yum -y install openssh-server

RUN useradd remote_user && \
    echo "remote_user:1234" | chpasswd && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user -R /home/remote_user/.ssh/ && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

RUN ssh-keygen -A

RUN rm -rf /run/nologin

RUN yum -y install mysql
RUN yum -y install unzip
RUN yum -y install sudo
RUN yum -y install python3

RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
RUN unzip awscli-bundle.zip
RUN sudo /usr/bin/python3.6 awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

CMD /usr/sbin/sshd -D


