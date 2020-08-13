#
# FusionAuth App Dockerfile
#
# Build:
#   > docker build -t fusionauth/fusionauth-app:1.18.0 .
#   > docker build -t fusionauth/fusionauth-app:latest .
#
# Run:
#  > docker run -p 9011:9011 -it fusionauth/fusionauth-app
#
# Publish:
#   > docker push fusionauth/fusionauth-app:1.18.0
#   > docker push fusionauth/fusionauth-app:latest
#

FROM fusionauth/fusionauth-java:14-jdk-alpine

###### Get and install FusionAuth App Bundle ########################
ENV FUSIONAUTH_VERSION=1.18.0
RUN apk add --no-cache bash curl unzip \
  && curl -Sk --progress-bar https://storage.googleapis.com/inversoft_products_j098230498/products/fusionauth/${FUSIONAUTH_VERSION}/fusionauth-app-${FUSIONAUTH_VERSION}.zip -o fusionauth-app.zip \
  && mkdir -p /usr/local/fusionauth/fusionauth-app \
  && unzip -nq fusionauth-app.zip -d /usr/local/fusionauth \
  && addgroup fusionauth \
  && adduser -G fusionauth -D -H fusionauth \
  && mkdir -p /usr/local/fusionauth/logs \
  && touch /usr/local/fusionauth/logs/fusionauth-app.log \
  && chown -R fusionauth:fusionauth /usr/local/fusionauth \
  && ln -sf /dev/stdout /usr/local/fusionauth/logs/fusionauth-app.log

###### Start FusionAuth App #########################################
LABEL description="Create an image running FusionAuth App. Installs FusionAuth App"
LABEL maintainer="FusionAuth <dev@fusionauth.io>"
EXPOSE 9011
USER fusionauth
ENV FUSIONAUTH_USE_GLOBAL_JAVA=1
CMD ["/usr/local/fusionauth/fusionauth-app/apache-tomcat/bin/catalina.sh", "run"]
