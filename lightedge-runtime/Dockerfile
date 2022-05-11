## build : docker build -t lightedge-runtime .
## run :   docker run --rm -it lightedge-runtime

FROM ubuntu:19.04
MAINTAINER Giovanni Baggio <g.baggio@fbk.eu>

RUN sed -i -e 's/archive.ubuntu.com\|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list

# Installing python dependencies
RUN buildDeps='python3-pip wget curl unzip' \
    && set -x \
    && apt-get update \
    && apt-get install -y $buildDeps \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install empower-core==1.0.5 \
    && pip3 install tornado==6.0.4 \
    && pip3 install pymodm==0.4.2 \
    && pip3 install influxdb==5.3.0 \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install nano \
    && apt-get install influxdb \
    && apt-get  install influxdb-client \
    && pip3 install python-stdnum==1.13 \
    && pip3 install PyYAML==5.1.2 \
    && pip3 install jsonpath-ng==1.5.1 \
    && pip3 install helmpythonclient==1.1 \
    && wget https://github.com/lightedge/lightedge-runtime/archive/master.zip \
    && unzip master.zip \
    && rm master.zip \
    && ln -sf /lightedge-runtime-master/conf/ /etc/lightedge \
    && mkdir -p /var/www/ \
    && ln -s /lightedge-runtime-master/webui/ /var/www/lightedge

# Installing Helm
RUN wget -O get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
RUN chmod 700 get_helm.sh
RUN ./get_helm.sh --no-sudo --version v3.2.1

# Cleanup
RUN apt-get purge -y --auto-remove $buildDeps
RUN rm get_helm.sh

#RUN chmod +x  /lightedge-runtime-master/lightedge-runtime.py


# Run the controller

#ENTRYPOINT ["python3.8", "/lightedge-runtime-master/lightedge-runtime.py"]
#ENTRYPOINT ["./lightedge-runtime-master/lightedge-runtime.py"]
# Expose Web GUI
EXPOSE 8888

# Expose UPF Manager
EXPOSE 7000

# Expose Influxdb
#EXPOSE 8086
