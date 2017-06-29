#################################################################
# Dockerfile
#
# Software:     JABAWS
# Version:      2.2
# Description:  JABAWS Distributed Web Services for Bioinformatics
# Website:      http://www.compbio.dundee.ac.uk/jabaws/, http://www.compbio.dundee.ac.uk/jabaws22/
# Provides:     jabaws
# Base Image:   openjdk:8-jre, tomcat:8.5
# Build Cmd:    docker build -t biomadeira/jabaws:2.2 .
# Push Cmd:     docker push biomadeira/jabaws:2.2
# Pull Cmd:     docker pull biomadeira/jabaws:2.2
# Run Cmd:      docker run --rm -it -p 8080:8080 biomadeira/jabaws:2.2
# Exit Signal:  Ctr-C
#################################################################

# Base Image
FROM tomcat:8.5
MAINTAINER Fábio Madeira "fabiomadeira@me.com"

################## BEGIN INSTALLATION ######################

# Install required packages
RUN apt-get update; apt-get -y install g++ && apt-get -y install make && \
    apt-get -y install libargtable2-dev && apt-get -y install gfortran

RUN wget --no-check-certificate https://www.python.org/ftp/python/2.7.13/Python-2.7.13.tgz && \
    tar -xzf Python-2.7.13.tgz && cd Python-2.7.13 && ./configure && make && make install

# Cleaning...
RUN apt-get clean && apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Deploy the JABAWS WAR
ENV WAR http://www.compbio.dundee.ac.uk/jabaws22/archive/jabaws.war
RUN wget $WAR -O ./jabaws.war
RUN mkdir -p $CATALINA_HOME/webapps/jabaws
RUN unzip ./jabaws.war -d $CATALINA_HOME/webapps/jabaws

# Update JABAWS configuration
ENV EXEC http://www.compbio.dundee.ac.uk/jabaws22/archive/docker/Executable.properties
RUN wget $EXEC -O ./Executable.properties
RUN mv ./Executable.properties $CATALINA_HOME/webapps/jabaws/conf/

# Create Jobs Output directory
RUN mkdir -p $CATALINA_HOME/webapps/jabaws/jobsout

# Compile/chmod the binaries
WORKDIR $CATALINA_HOME/webapps/jabaws/binaries/src/
#RUN chmod +x ./compilebin.sh && ./compilebin.sh
RUN chmod +x ./setexecflag.sh && ./setexecflag.sh
WORKDIR $CATALINA_HOME

# Default command to execute at startup of the container
EXPOSE 8080
CMD ["catalina.sh", "run"]
