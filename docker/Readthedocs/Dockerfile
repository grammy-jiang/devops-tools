FROM ubuntu:16.04
LABEL maintainer "grammy.jiang@gmail.com"

# change apt source to the one in china
COPY ./sources.list /etc/apt/

# add git user and proxy
COPY ./gitconfig /root/.gitconfig

# change pip source to douban
RUN mkdir /root/.pip/ \
 && echo '[global]' >> /root/.pip/pip.conf \
 && echo 'index-url = https://pypi.douban.com/simple' >> /root/.pip/pip.conf

RUN apt-get update \
 && apt-get install -y \
    build-essential \
    python-dev \
    python-pip \
    python-setuptools \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    elasticsearch \
    redis-server \
    git

RUN git clone https://github.com/rtfd/readthedocs.org.git

RUN cd readthedocs.org \
 && pip install --upgrade pip \
 && pip install --requirement requirements.txt

RUN cd readthedocs.org \
 && python manage.py migrate \
 && echo "from django.contrib.auth.models import User; User.objects.create_superuser('admin', 'admin@localhost', 'admin')" | ./manage.py shell

ENTRYPOINT ["python", "readthedocs.org/manage.py", "runserver", "0.0.0.0:80"]
