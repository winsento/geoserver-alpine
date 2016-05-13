FROM anapsix/alpine-java:jdk7
MAINTAINER winsent <pipetc@gmail.com>

ENV GEOSERVER_VERSION 2.8.3
ENV GDAL_VERSION 1.11.4
ENV ANT_VERSION 1.9.7
ENV LD_LIBRARY_PATH /usr/local/lib/
ENV GEOSERVER_HOME /opt/geoserver

RUN apk --update --no-cache add gcc  g++ make swig && \
    wget http://download.osgeo.org/gdal/${GDAL_VERSION}/gdal-${GDAL_VERSION}.tar.gz -O /tmp/gdal.tar.gz && \
    tar xzf /tmp/gdal.tar.gz -C /tmp && \
    cd /tmp/gdal-${GDAL_VERSION} && ./configure  --with-java=$JAVA_HOME && make && make install

# Install Apacvhe Ant
RUN cd /tmp && \
    wget http://mirrors.ae-online.de/apache/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz -O /tmp/ant.tar.gz && \
    tar xzf /tmp/ant.tar.gz -C /tmp && rm /tmp/ant.tar.gz && \
    ln -s /tmp/apache-ant-${ANT_VERSION}/bin/ant /usr/local/bin/ant

# Install GDAL Java binding
RUN cd /tmp/gdal-${GDAL_VERSION}/swig/java && \
    sed -i '/JAVA_HOME =/d' java.opt && \
    make && make install && \
    cp *.so /usr/local/lib/ && \
    rm -rf /tmp/build
 
# Get native JAI and ImageIO
RUN \
    cd $JAVA_HOME && \
    wget http://data.boundlessgeo.com/suite/jai/jai-1_1_3-lib-linux-amd64-jdk.bin && \
    echo "yes" | sh jai-1_1_3-lib-linux-amd64-jdk.bin && \
    rm jai-1_1_3-lib-linux-amd64-jdk.bin

RUN \
    cd $JAVA_HOME && \
    export _POSIX2_VERSION=199209 &&\
    wget http://data.opengeo.org/suite/jai/jai_imageio-1_1-lib-linux-amd64-jdk.bin && \
    echo "yes" | sh jai_imageio-1_1-lib-linux-amd64-jdk.bin && \
    rm jai_imageio-1_1-lib-linux-amd64-jdk.bin

# Get GeoServer
RUN wget -c http://downloads.sourceforge.net/project/geoserver/GeoServer/$GEOSERVER_VERSION/geoserver-$GEOSERVER_VERSION-bin.zip -O ~/geoserver.zip && \
    unzip ~/geoserver.zip -d /opt && mv -v /opt/geoserver* /opt/geoserver && \
    rm ~/geoserver.zip

# Get OGR plugin
RUN wget -c http://downloads.sourceforge.net/project/geoserver/GeoServer/$GEOSERVER_VERSION/extensions/geoserver-$GEOSERVER_VERSION-ogr-wfs-plugin.zip -O ~/geoserver-ogr-plugin.zip &&\
    unzip -o ~/geoserver-ogr-plugin.zip -d /opt/geoserver/webapps/geoserver/WEB-INF/lib/ && \
    rm ~/geoserver-ogr-plugin.zip

# Get GDAL plugin
RUN wget -c http://downloads.sourceforge.net/project/geoserver/GeoServer/$GEOSERVER_VERSION/extensions/geoserver-$GEOSERVER_VERSION-gdal-plugin.zip -O ~/geoserver-gdal-plugin.zip &&\
    unzip -o ~/geoserver-gdal-plugin.zip -d /opt/geoserver/webapps/geoserver/WEB-INF/lib/ && \
    rm ~/geoserver-gdal-plugin.zip

# Replace GDAL Java bindings
RUN rm -rf $GEOSERVER_HOME/webapps/geoserver/WEB-INF/lib/imageio-ext-gdal-bindings-1.9.2.jar
RUN cp /tmp/gdal-${GDAL_VERSION}/swig/java/gdal.jar $GEOSERVER_HOME/webapps/geoserver/WEB-INF/lib/gdal.jar

# Expose GeoServer's default port
EXPOSE 8080
CMD ["/opt/geoserver/bin/startup.sh"]
