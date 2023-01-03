#ARG BUILD_FROM
#FROM $BUILD_FROM

#FROM selenium/standalone-firefox:4.5.0
FROM seleniarm/standalone-chromium:4.7.2

USER root

# No interactive frontend during docker build
ENV DEBIAN_FRONTEND=noninteractive \
    DEBCONF_NONINTERACTIVE_SEEN=true

RUN apt-get -qqy update \
  && apt-get -qqy --no-install-recommends install \
    python3-pip \
    nano \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

# Add Python dependencies
RUN python3 -m pip install selenium-wire requests Flask Flask-RESTful

#======================================
# Add Supervisor configuration file
#======================================
COPY pyapi.conf /etc/supervisor/conf.d/

#===================================================
# Run the following commands as non-privileged user
#===================================================
USER 1200:1201

COPY pyapi.py /home/seluser/pyapi.py

EXPOSE 5000