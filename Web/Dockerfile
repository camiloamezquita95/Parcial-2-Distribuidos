FROM ubuntu
RUN apt-get update && apt-get install -y \
        gcc \
        python \
        python2.7-dev \
        postgresql-server-dev-9.5 \
        wget
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install virtualenv 
RUN echo "root:docker" | chpasswd
RUN useradd -ms /bin/bash flask
USER flask
WORKDIR /home/flask
RUN virtualenv flask_env
RUN mkdir smartlabs
COPY requirements.txt /home/flask/smartlabs/
COPY app.py /home/flask/smartlabs/
COPY script.sh /home/flask/smartlabs/
USER root
RUN echo "sh /home/flask/smartlabs/script.sh" >> /etc/rc.local
EXPOSE 80
CMD ["sh","/home/flask/smartlabs/script.sh"]  