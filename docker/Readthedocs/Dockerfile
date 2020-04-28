FROM ubuntu:16.04@sha256:a4fc0c40360ff2224db3a483e5d80e9164fe3fdce2a8439d2686270643974632
LABEL maintainer "grammy.jiang@gmail.com"

# change apt source to the one in china
COPY ./sources.list /etc/apt/

# add git user and proxy
COPY ./gitconfig /root/.gitconfig

# change pip source to douban
RUN echo '[global]' >> /etc/pip.conf \
 && echo 'index-url = https://pypi.douban.com/simple' >> /etc/pip.conf

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
