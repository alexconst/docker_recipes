FROM ubuntu:wily

# install packages
RUN apt-get update && \
    apt-get install -y \
        ruby-dev \
        bundler \
        zlib1g-dev \
        ruby-execjs \
        --no-install-recommends && \
    apt-get install -y \
        python2.7-dev
        python-pygments
# install gems
RUN gem install activesupport
RUN gem install github-pages -v 43
# cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*
# fix locale
RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales
RUN echo 'export LC_ALL="en_US.UTF-8"' >> $HOME/.bashrc
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

# informs Docker that the container listens on the specified network ports at runtime
# and makes this port available to processes inside the container
EXPOSE 4000

# set workdir for any commands below
# with /shared/ being the guest volume dir when a container is spinned
WORKDIR /shared/blog/
# setting an entrypoint will set the container to run as an executable
ENTRYPOINT ["jekyll"]
# so everytime a container is created, it will cd to WORKDIR and run ENTRYPOINT

