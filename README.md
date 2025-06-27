# FreeSWITCH 1.10.12

## Install FreeSWITCH on Debian 12

SignalWire **Personal Access Tokens** (PAT)s are required to access FreeSWITCH install packages: [HOWTO Create a SignalWire Personal Access Token](https://freeswitch.org/confluence/display/FREESWITCH/HOWTO+Create+a+SignalWire+Personal+Access+Token).

	TOKEN=pat_YOUR_SIGNALWIRE_TOKEN

	wget --http-user=signalwire --http-password=$TOKEN -O /usr/share/keyrings/signalwire-freeswitch-repo.gpg https://freeswitch.signalwire.com/repo/deb/debian-release/signalwire-freeswitch-repo.gpg
	echo "machine freeswitch.signalwire.com login signalwire password $TOKEN" > /etc/apt/auth.conf.d/freeswitch.conf
	echo "deb [signed-by=/usr/share/keyrings/signalwire-freeswitch-repo.gpg] https://freeswitch.signalwire.com/repo/deb/debian-release/ `lsb_release -sc` main" > /etc/apt/sources.list.d/freeswitch.list
	echo "deb-src [signed-by=/usr/share/keyrings/signalwire-freeswitch-repo.gpg] https://freeswitch.signalwire.com/repo/deb/debian-release/ `lsb_release -sc` main" >> /etc/apt/sources.list.d/freeswitch.list

	apt-get update
	apt-get install -qqy --no-install-recommends imagemagick librabbitmq4 \
		freeswitch freeswitch-mod-av freeswitch-mod-opus freeswitch-mod-sndfile \
		freeswitch-mod-shout freeswitch-mod-sofia freeswitch-mod-dialplan-xml \
		freeswitch-mod-valet-parking freeswitch-mod-conference freeswitch-mod-opusfile \
		freeswitch-mod-console freeswitch-mod-event-socket freeswitch-mod-loopback \
		freeswitch-mod-commands freeswitch-mod-db freeswitch-mod-dptools \
		freeswitch-mod-expr freeswitch-mod-hash freeswitch-mod-spandsp \
		freeswitch-mod-imagick freeswitch-mod-png freeswitch-mod-native-file \
		freeswitch-mod-local-stream freeswitch-mod-tone-stream freeswitch-mod-lua \
		freeswitch-mod-http-cache freeswitch-mod-spy freeswitch-music-default \
		freeswitch-mod-json-cdr freeswitch-mod-logfile freeswitch-systemd \


	mkdir /var/cache/freeswitch && chmod -R 777 /var/cache/freeswitch

## Install config files

    cd /etc/freeswitch
    curl https://raw.githubusercontent.com/herbiel/freeswitch-mini/refs/heads/main/mime.types \
        -o mime.types
    curl https://raw.githubusercontent.com/herbiel/freeswitch-mini/refs/heads/main/configuration.xml \
        -o configuration.xml
    curl https://raw.githubusercontent.com/herbiel/freeswitch-mini/refs/heads/main/freeswitch.xml \
        -o freeswitch.xml
    curl https://raw.githubusercontent.com/herbiel/freeswitch-mini/refs/heads/main/vars.xml \
        -o vars.xml

Change IP in the `vars.xml` , `external_sip_ip` 

## Run FreeSWITCH

    systemctl enable freeswitch
    systemctl start freeswitch

