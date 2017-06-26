### JABAWS 2.2 ###

FROM tomcat:8.5-alpine

ENV WAR http://www.compbio.dundee.ac.uk/jabaws22/archive/jabaws.war
RUN wget $WAR -O ./jabaws.war
RUN mkdir -p $CATALINA_HOME/webapps/jabaws
RUN unzip ./jabaws.war -d $CATALINA_HOME/webapps/jabaws

WORKDIR $CATALINA_HOME/webapps/jabaws/binaries/src/

# compile the binaries
#RUN chmod +x ./compilebin.sh && ./compilebin.sh
RUN chmod +x ./setexecflag.sh && ./setexecflag.sh

WORKDIR $CATALINA_HOME

# make missing dirs
RUN mkdir -p $CATALINA_HOME/webapps/jabaws/jobsout

EXPOSE 8080
CMD ["catalina.sh", "run"]
