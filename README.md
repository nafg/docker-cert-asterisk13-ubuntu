##### Docker image with Certified Asterisk 13 LTS version and Fail2ban on Ubuntu 64bits (14.04.2 LTS)

This is the Docker Certified Asterisk 13.1-cert2 version on Ubuntu X86_64 with SIP and new PJSIP channels. Certified Asterisk 13 is the latest LTS version recommended for production systems with a release frequency of 2 - 4 times per year.

Image size: 534.9 MB

It includes:

- Certified Asterisk 13.1-cert2
- Sip and new pjsip channel enabled
- Only g729, alaw, ulaw english sounds and MOH
- Fail2ban (v0.8.11)

To pull it:

`# docker pull cleardevice/docker-cert-asterisk13-ubuntu`

For compile it on your own platform/server from the Dockerfile:

`$ git clone https://github.com/cleardevice/docker-cert-asterisk13-ubuntu`

`$ cd docker-cert-asterisk13-ubuntu`

`$ docker build -t myrepository/asterisk01 .`

To execute it:

Asterisk PBX needs to use a big range of ports, so it needs to be executed with docker version 1.5.0 or higher (available in docker ubuntu sources) for being able to launch the image specifying a range of ports. For example:

`# docker run --restart=always --name asterisk01 -d -p 5060-5065:5060-5065/tcp -p 10000-10500:10000-10500/udp cleardevice/docker-cert-asterisk13-ubuntu`

and connect to asterisk CLI with:

`# docker exec -t -i asterisk01 asterisk -rvvvvv`

Notice:

> Seems that opening too much ports in a docker images, consumes a lot of resources in your docker host and may fail to launch it. So giving that every SIP call can use up to 4 RTP ports, it is convenient to open only the necessary RTP ports for the expected calls. In this case we open 500 RTP ports for 125 expected concurrent calls. From 10000 to 10500. Don't forget to configure that RTP ports in the /etc/asterisk/rtp.conf file:

```
# rtpstart=10000
# rtpend=10500
```

### Thanks ###

- Gonzalo Marcote for idea (https://github.com/gonzalomarcote/docker-cert-asterisk13-centos7)
- Dave Beckett for install script idea (https://github.com/dajobe/docker-nghttp2) 
