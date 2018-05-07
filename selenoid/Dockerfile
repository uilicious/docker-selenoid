# Entrypoint for aerokube/selenoid
# https://github.com/aerokube/selenoid/blob/master/Dockerfile

FROM aerokube/selenoid:1.3.4


#
# File data for which selenoid would use
#
ENV BROWSER_JSON ""


#
# Prepares the selenoid file runner script
#
RUN echo '#!/bin/bash'                                                > /entrypoint/file-runner.sh && \
	echo ''                                                           >> /entrypoint/file-runner.sh && \
	echo 'if [ -n "$BROWSER_JSON" ]; then '                           >> /entrypoint/file-runner.sh && \
	echo '   echo "###"'                                              >> /entrypoint/file-runner.sh && \
	echo '   echo "### using browser_json"'                           >> /entrypoint/file-runner.sh && \
	echo '   echo "###"'                                              >> /entrypoint/file-runner.sh && \
	echo '   mkdir -p /etc/selenoid/;'                                >> /entrypoint/file-runner.sh && \
	echo '   echo "$BROWSER_JSON" > /etc/selenoid/browsers.json'      >> /entrypoint/file-runner.sh && \
	echo 'fi '                                                        >> /entrypoint/file-runner.sh && \
	echo 'exec "$@"'                                                  >> /entrypoint/file-runner.sh && \
	chmod +x /entrypoint/file-runner.sh;


ENTRYPOINT ["/entrypoint/file-runner.sh", /usr/bin/selenoid", "-listen", ":4444", "-conf", "/etc/selenoid/browsers.json", "-video-output-dir", "/opt/selenoid/video/"]