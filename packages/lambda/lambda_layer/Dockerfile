#
# Build with:
# docker build --compress -t adieuadieu/chromium-for-amazonlinux-base:62.0.3202.62 --build-arg VERSION=62.0.3202.62 .
#
# Jump into the container with:
# docker run -i -t --rm --entrypoint /bin/bash  adieuadieu/chromium-for-amazonlinux-base
#
# Launch headless Chromium with:
# docker run -d --rm --name headless-chromium -p 9222:9222 adieuadieu/headless-chromium-for-aws-lambda
#

ARG VERSION
ARG HOME
#ENV HOME=${HOME:-master}
#ENV VERSION ${VERSION:-master}

#FROM headless-chrome:${VERSION}
#FROM headless-chromium:${VERSION}
#FROM headless-chromium:90.0.4430.72
#FROM headless-chromium:94.0.4606.81
FROM headless-chromium:${VERSION}

ARG CHROME_DRIVER_VERSION

WORKDIR /

#RUN amazon-linux-extras install epel && \
#  yum update && \
#  echo "install epel-release repo."

#RUN yum install -y chromium chromium-common
RUN yum install -y awscli
RUN mkdir -p /root/.aws

ADD build.sh /

# copy aws user's credentials
#ADD ${HOME}/.aws ${HOME}/
COPY aws /root/.aws

CMD [echo "${CHROME_DRIVER_VERSION}"]

# build distfile.zip
RUN sh /build.sh

