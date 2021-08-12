FROM adoptopenjdk/openjdk16:centos
LABEL maintainer="Blaž Mrak, github.com/blazmrak" description="Eclipse Jakarta EE Glassfish v6 release image"
ENV GLASSFISH_ARCHIVE glassfish6
ENV DOMAIN_NAME domain1
ENV INSTALL_DIR /opt
RUN useradd -b /opt -m -s /bin/sh -d ${INSTALL_DIR} serveradmin && echo serveradmin:serveradmin | chpasswd
RUN yum -y install unzip   \
    && curl -o ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}.zip -L https://download.eclipse.org/ee4j/glassfish/glassfish-6.2.0.zip \
    && unzip ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}.zip -d ${INSTALL_DIR} \
    && rm ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}.zip \
    && chown -R serveradmin:serveradmin /opt \
    && chmod -R a+rw /opt
ENV GLASSFISH_HOME ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}/glassfish
ENV DEPLOYMENT_DIR ${GLASSFISH_HOME}/domains/domain1/autodeploy
WORKDIR ${GLASSFISH_HOME}/bin
ENTRYPOINT ./asadmin start-domain --verbose ${DOMAIN_NAME}
USER serveradmin
EXPOSE 4848 8009 8080 8181
