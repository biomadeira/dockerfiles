# JABAWS test Dockerfile
# 13.03.2017

FROM tomcat:8.5-alpine
ENV jabaws_war http://www.compbio.dundee.ac.uk/user/www-jws2/servers/jabaws.war
RUN wget $jabaws_war -O ./jabaws.war
ADD ./jabaws.war $CATALINA_HOME/webapps/

EXPOSE 8080
CMD ["catalina.sh", "run"]
