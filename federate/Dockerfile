FROM prom/prometheus:v2.4.0

#### ARGS ####

ARG scrapeinterval
ARG evaluationinterval
ARG scrapetimeout
ARG tsdbretention
# rulespath defines the rules folder a prometheus instance of this image will be using
ARG rulespath
# startupfile defines the file path of the startup script
ARG startupfile
ARG prometheusname
ARG federatetargets
ARG federatehostprefix
ARG federatehostsufix

#### ENVS ####

# global envs
ENV SCRAPE_INTERVAL ${scrapeinterval}
ENV EVALUATION_INTERVAL ${evaluationinterval}
ENV SCRAPE_TIMEOUT ${scrapetimeout}
# tsdb storage envs
ENV TSDB_RETENTION ${tsdbretention}
# PROMETHEUS_NAME identifies the prometheus instance
ENV PROMETHEUS_NAME ${prometheusname}
# FEDERATE_TARGETS_BLUE identifies the blue deployment region federate targets
ENV FEDERATE_TARGETS ${federatetargets}
# FEDERATE_HOST_SUFIX the host name prefix that will be appended to the targets. can be empty
ENV FEDERATE_HOST_PREFIX ${federatehostprefix}
# FEDERATE_HOST_SUFIX the host name sufix that will be appended to the targets. can be empty
ENV FEDERATE_HOST_SUFIX ${federatehostsufix}

#### CONFIG ####

USER root

ADD $rulespath /etc/prometheus/
ADD $startupfile /

ADD prometheus.yml /etc/prometheus/
ADD build.sh /

RUN chmod -R 777 /etc/prometheus/
RUN chmod -R 777 /startup.sh
RUN chmod +x /build.sh

RUN sh /build.sh /etc/prometheus/

ENTRYPOINT [ "/bin/sh" ]
CMD [ "/startup.sh" ]