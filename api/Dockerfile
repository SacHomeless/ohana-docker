FROM ubuntu

RUN apt-get update

RUN apt-get install -y openssh-server git-core openssh-client curl
RUN apt-get install -y vim
RUN apt-get install -y build-essential
RUN apt-get install -y openssl libreadline6 libreadline6-dev curl zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev automake libtool bison pkg-config
RUN apt-get install -y gawk libgdbm-dev libgmp-dev libgdm-dev libffi-dev

RUN apt-get install -y libpq-dev
RUN apt-get install -y postgresql-client
RUN apt-get install -y nodejs

RUN adduser --disabled-password sacsos

USER sacsos

RUN mkdir /home/sacsos/api

WORKDIR /home/sacsos/api

# install RVM, Ruby, and Bundler
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN \curl -L https://get.rvm.io | bash -s stable
RUN /bin/bash -l -c "rvm install --autolibs=fail 2.2.3"
RUN /bin/bash -l -c "echo 'gem: --no-document' > ~/.gemrc"

run git clone https://github.com/SacHomeless/ohana-api.git .

RUN /bin/bash -l -c "rvm gemset create ohana-api"
RUN /bin/bash -l -c "rvm gemset use ohana-api && gem install bundler && bundle install"
RUN /bin/bash -l -c "rvm gemset use ohana-api && gem pristine bcrypt"

USER root
COPY ./files/application.yml config/
COPY ./files/database.yml    config/
COPY ./files/settings.yml    config/
COPY ./files/pgpass          /home/sacsos/.pgpass
RUN /bin/bash -lc "chown sacsos:sacsos /home/sacsos/.pgpass"
USER sacsos
RUN /bin/bash -l -c "chmod 0600 /home/sacsos/.pgpass"

EXPOSE 3000

CMD /bin/bash -l -c "rails s -b 0.0.0.0"
