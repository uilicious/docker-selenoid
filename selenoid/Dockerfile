# Entrypoint for aerokube/selenoid
# https://github.com/aerokube/selenoid/blob/master/Dockerfile

FROM aerokube/selenoid:1.3.4


#
# File data for which selenoid would use
#
ENV BROWSER_JSON '{ "chrome": { "default": "63.0", "versions": { "63.0": { "image": "uilicious/selenoid-chrome:63.0", "port": "4444", "path": "/", "tmpfs": { "/tmp": "size=2048m" } } } }, "firefox": { "default": "57.0", "versions": { "57.0": { "image": "uilicious/selenoid-firefox:57.0", "port": "4444", "path": "/wd/hub", "tmpfs": { "/tmp": "size=2048m" } } } } }'


#
# Prepares the selenoid file runner script
#
RUN echo '#!/bin/sh'                                                > /entrypoint.sh && \
	echo ''                                                           >> /entrypoint.sh && \
	echo 'if [ -n "$BROWSER_JSON" ]; then '                           >> /entrypoint.sh && \
	echo '   echo "###"'                                              >> /entrypoint.sh && \
	echo '   echo "### using browser_json"'                           >> /entrypoint.sh && \
	echo '   echo "###"'                                              >> /entrypoint.sh && \
	echo '   mkdir -p /etc/selenoid/;'                                >> /entrypoint.sh && \
	echo '   echo "$BROWSER_JSON" > /etc/selenoid/browsers.json'      >> /entrypoint.sh && \
	echo 'fi '                                                        >> /entrypoint.sh && \
	echo 'exec "$@"'                                                  >> /entrypoint.sh && \
	chmod +x /entrypoint.sh;


ENTRYPOINT ["/entrypoint.sh", "/usr/bin/selenoid", "-listen", ":4444", "-conf", "/etc/selenoid/browsers.json"]