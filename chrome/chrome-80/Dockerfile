FROM selenoid/chrome:80.0

# Using root user for installation
USER root

# Listing language pack used for installation (for refrence)
RUN echo "Installing the following language packs" && echo $(apt-cache --names-only search ^language-pack-* | awk '{ print $1 }' | grep -v language-pack-touch-* | grep -v language-pack-gnome-* | grep -v language-pack-kde-*)

# Actual language-pack installaation
RUN apt-get update && apt-get install -y $(apt-cache --names-only search ^language-pack-* | awk '{ print $1 }' | grep -v language-pack-touch-* | grep -v language-pack-gnome-* | grep -v language-pack-kde-*)

# Install any needed font (if needed)
RUN apt-get update && apt-get install -y fonts-arphic-ukai fonts-arphic-uming fonts-ipafont-mincho fonts-ipafont-gothic fonts-unfonts-core

# Install emoji font
RUN apt-get update && apt-get install -y fonts-noto-color-emoji

# Copy over the entrypoint script
COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh && chmod 0755 /entrypoint.sh

# Reverting back to selenium user
USER selenium