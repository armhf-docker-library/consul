FROM armhfbuild/alpine:3.3

ENV CONSUL_ARCH arm
ENV CONSUL_VERSION 0.6.3
ENV CONSUL_SHA256 c5fd5278be2757d2468bc7e263af15bc9a9e80fc5108fec658755804ea9bca56

RUN apk --update add curl && \
  curl -fsSL https://github.com/armhf-docker-library/glibc/releases/download/2.22/glibc-bin.tar.gz \
    | tar -xz -C /

RUN curl -fsSL -o /tmp/consul.zip \
    https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_${CONSUL_ARCH}.zip \
  && echo "${CONSUL_SHA256}  /tmp/consul.zip" | sha256sum -c \
  && cd /bin \
  && unzip /tmp/consul.zip \
  && chmod +x /bin/consul \
  && rm /tmp/consul.zip

ENTRYPOINT ["/bin/consul"]
