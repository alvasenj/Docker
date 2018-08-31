FROM ubuntu:16.04

RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    apache2 php7.0 php7.0-mysql libapache2-mod-php7.0 curl lynx-cur \
	&& rm -r /var/lib/apt/lists/*

# Enable apache mods.
RUN a2enmod php7.0
RUN a2enmod rewrite

# Update the PHP.ini file, enable <? ?> tags and quieten logging.
RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php/7.0/apache2/php.ini
RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php/7.0/apache2/php.ini

RUN mkdir /repo
COPY aplicacion/index.html /repo/
COPY virtualhosts-com-save.conf /etc/apache2/sites-available
RUN cd /etc/apache2/sites-available/
RUN a2dissite 000-default.conf 
RUN a2ensite virtualhosts-com-save.conf

# Default command	
CMD ["apachectl", "-D", "FOREGROUND"]

# Ports
EXPOSE 80
