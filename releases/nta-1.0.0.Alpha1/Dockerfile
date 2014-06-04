FROM fedora

RUN yum -y update

RUN yum -y install java-1.7.0-openjdk-devel

RUN yum clean all

RUN cd /opt

RUN curl http://download.jboss.org/wildfly/8.0.0.Final/wildfly-8.0.0.Final.tar.gz | tar xz

# Create the wildfly user and group
RUN groupadd -r wildfly -g 433 && useradd -u 431 -r -g wildfly -d /opt/wildfly-8.0.0.Final -s /sbin/nologin -c "WildFly user" wildfly

# Change the owner of the /opt/wildfly directory
RUN chown -R wildfly:wildfly /opt/wildfly-8.0.0.Final

RUN curl http://www.jboss.org/file-access/default/members/jbosstm/downloads/nta/1.0.0.Alpha1/binary/nta-full.ear >/opt/wildfly-8.0.0.Final/standalone/deployments/nta-full.ear

RUN curl http://www.jboss.org/file-access/default/members/jbosstm/downloads/nta/1.0.0.Alpha1/binary/demo.war >/opt/wildfly-8.0.0.Final/standalone/deployments/demo.war

# Expose the ports we're interested in
EXPOSE 8080 9990

# Run everything below as the wildfly user
USER wildfly

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/wildfly-8.0.0.Final/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
