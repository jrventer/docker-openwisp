FROM alpine:3.16

WORKDIR /opt/openwisp/
RUN apk add --no-cache --upgrade \
            openssl~=1.1.1s-r0 \
            cyrus-sasl~=2.1.28-r1	\
            cyrus-sasl-login~=2.1.28-r1 && \
    apk add --no-cache \
            postfix~=3.7.3-r0 \
            rsyslog~=8.2204.1-r0	 \
            tzdata~=2022f-r1 && \
    rm -rf /tmp/* /var/cache/apk/*

CMD ["sh", "init_command.sh"]
EXPOSE 25

COPY ./openwisp_postfix/rsyslog.conf /etc/rsyslog.conf
COPY ./common/init_command.sh \
    ./common/utils.sh \
    /opt/openwisp/

ENV MODULE_NAME=postfix \
    TZ=UTC \
    POSTFIX_MYHOSTNAME=example.org \
    POSTFIX_ALLOWED_SENDER_DOMAINS=example.org \
    POSTFIX_RELAYHOST=null \
    POSTFIX_DESTINATION='$mydomain, $myhostname' \
    POSTFIX_RELAYHOST_USERNAME=null \
    POSTFIX_RELAYHOST_PASSWORD=null \
    POSTFIX_RELAYHOST_TLS_LEVEL=may \
    POSTFIX_MYNETWORKS='127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128' \
    POSTFIX_MESSAGE_SIZE_LIMIT=0 \
    POSTFIX_DEBUG_MYNETWORKS=null
