FROM alpine:3.3
MAINTAINER Gareth Rushgrove "gareth@puppet.com"

ENV PUPPET_VERSION="4.4.2" FACTER_VERSION="2.4.6"

LABEL com.puppet.version=$PUPPET_VERSION com.puppet.git.repo="https://github.com/puppetlabs/dockerfiles" com.puppet.git.sha="ca4b5726dd0e244b04ed7f84d6568f79943c91ce" com.puppet.buildtime="2016-05-29T08:18:48Z" com.puppet.dockerfile="/Dockerfile"

RUN apk add --update ruby ruby-rdoc ruby-irb ca-certificates && \
    echo http://dl-4.alpinelinux.org/alpine/edge/testing/ >> /etc/apk/repositories && \
    apk add --update shadow && \
    rm -rf /var/cache/apk/* && \
    gem install puppet:"$PUPPET_VERSION" facter:"$FACTER_VERSION" && \
    /usr/bin/puppet module install puppetlabs-apk

# Workaround for https://tickets.puppetlabs.com/browse/FACT-1351
RUN rm /usr/lib/ruby/gems/2.2.0/gems/facter-"$FACTER_VERSION"/lib/facter/blockdevices.rb

ENTRYPOINT ["/usr/bin/puppet"]
CMD ["agent", "--verbose", "--onetime", "--no-daemonize", "--summarize" ]

COPY Dockerfile /
