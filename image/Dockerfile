FROM ubuntu:16.04

RUN apt-get update && apt-get clean && apt-get install -y \
    x11vnc \
    xvfb \
    fluxbox \
    wmctrl \
    wget \
    lsb-release \
    bzip2 \
    libdbus-glib-1-2 \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list \
    && echo "deb http://archive.canonical.com/ubuntu $(lsb_release -sc) partner" >> /etc/apt/sources.list \
    && apt-get update && apt-get -y install google-chrome-stable chromium-browser

RUN wget -P /tmp/firefox https://ftp.mozilla.org/pub/firefox/releases/82.0.3/linux-x86_64/en-US/firefox-82.0.3.tar.bz2 \
     && tar jxvf /tmp/firefox/firefox-82.0.3.tar.bz2 -C /usr/lib/ \
     && ln -s /usr/lib/firefox/firefox /usr/bin/firefox

#RUN apt-get install adobe-flashplugin



#RUN wget -P /tmp/flash https://fpdownload.macromedia.com/pub/labs/flashruntimes/flashplayer/linux64/flash_player_ppapi_linux.x86_64.tar.gz
#RUN wget -P /tmp/flash https://web.archive.org/web/20201209143013/https://fpdownload.macromedia.com/pub/labs/flashruntimes/flashplayer/linux64/flash_player_ppapi_linux.x86_64.tar.gz
RUN wget -P /tmp/flash https://web.archive.org/web/20200511125906/https://fpdownload.macromedia.com/pub/labs/flashruntimes/flashplayer/linux64/flash_player_ppapi_linux.x86_64.tar.gz \
    && mkdir /usr/lib/adobe-flashplugin/ \
    && echo "If this fail with not gzip try again (must be some error html from archive.org)" \
    && tar zxvf /tmp/flash/flash_player_ppapi_linux.x86_64.tar.gz -C /usr/lib/adobe-flashplugin/ \
    && echo "Flash installed (for chrome):"

RUN wget -P /tmp/flash-firefox https://web.archive.org/web/20200517100812/https://fpdownload.macromedia.com/pub/labs/flashruntimes/flashplayer/linux64/flash_player_npapi_linux.x86_64.tar.gz \
    && echo "If this fail with not gzip try again (must be some error html from archive.org)" \
    && mkdir /usr/lib/firefox/plugins/ \
    && tar zxvf /tmp/flash-firefox/flash_player_npapi_linux.x86_64.tar.gz -C /usr/lib/firefox/plugins/ libflashplayer.so \
    && tar zxvf /tmp/flash-firefox/flash_player_npapi_linux.x86_64.tar.gz -C / usr \
    && echo "Flash installed (for firefox):"
#RUN wget -P /tmp/flash https://web.archive.org/web/20200511125906/https://fpdownload.macromedia.com/pub/labs/flashruntimes/flashplayer/linux64/flash_player_ppapi_linux_debug.x86_64.tar.gz
#alternate link https://web.archive.org/web/20201209143013/https://fpdownload.macromedia.com/pub/labs/flashruntimes/flashplayer/linux64/flash_player_ppapi_linux.x86_64.tar.gz

#RUN apt-get install flashplugin-installer

#WORKDIR /
#RUN apt-get -y install git build-essential \
#    && git clone https://github.com/wolfcw/libfaketime.git
#WORKDIR /libfaketime/src
#RUN make install
#WORKDIR /

RUN useradd apps \
    && mkdir -p /home/apps \
    && chown -v -R apps:apps /home/apps

COPY bootstrap.sh /

RUN sed -i -e 's/\r$//' bootstrap.sh \
	&& chmod +x bootstrap.sh

CMD './bootstrap.sh'

#CMD ["/bin/sh", "-c", "LD_PRELOAD=/usr/local/lib/faketime/libfaketime.so.1 FAKETIME_NO_CACHE=1 FAKETIME='2019-05-01 12:00:00' ./bootstrap.sh"]
