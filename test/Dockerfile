FROM ubuntu:wily-20151019

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B07804338C015B73 && \
    echo 'deb https://sdkrepo.atlassian.com/debian/ stable contrib' | tee /etc/apt/sources.list.d/atlassian.list && \
    apt-get install apt-transport-https -y && \
    apt-get update && \
    apt-get install atlassian-plugin-sdk openjdk-8-jdk -y && \
    /var/lib/dpkg/info/ca-certificates-java.postinst configure && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    useradd -ms /bin/bash bamboo    
    

ENV USER_HOME /home/bamboo
ENV MAVEN_REPOSITORY $USER_HOME/.m2
ENV BAMBOO_PROJECT $USER_HOME/project

COPY bamboo $BAMBOO_PROJECT
RUN chown -hR bamboo $BAMBOO_PROJECT

USER bamboo
RUN mkdir -p $MAVEN_REPOSITORY && \
    ln -s /repository/ $MAVEN_REPOSITORY

EXPOSE 6990
WORKDIR $BAMBOO_PROJECT
CMD ["atlas-run"]

