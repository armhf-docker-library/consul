FROM alpine:3.3

ENV CONSUL_ARCH amd64
ENV CONSUL_VERSION 0.6.3
ENV CONSUL_SHA256 b0532c61fec4a4f6d130c893fd8954ec007a6ad93effbe283a39224ed237e250

RUN apk --update add curl ca-certificates && \
    curl -Ls https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk > /tmp/glibc-2.21-r2.apk && \
    apk add --allow-untrusted /tmp/glibc-2.21-r2.apk && \
    rm -rf /tmp/glibc-2.21-r2.apk /var/cache/apk/*

# RUN apk --update --no-cache add curl && \
#   curl -fsSL https://github.com/armhf-docker-library/glibc/releases/download/2.22/glibc-bin.tar.gz \
#     | tar -x -C /

RUN curl -fsSL -o /tmp/consul.zip \
    https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_${CONSUL_ARCH}.zip \
  && echo "${CONSUL_SHA256}  /tmp/consul.zip" | sha256sum -c \
  && cd /bin \
  && unzip /tmp/consul.zip \
  && chmod +x /bin/consul \
  && rm /tmp/consul.zip

ENTRYPOINT ["/bin/consul"]
